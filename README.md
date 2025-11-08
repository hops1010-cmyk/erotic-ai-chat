<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>18+ Chat — Online API Integration</title>
  <style>
    :root{
      --bg:#0e1720; --card:#111f28; --accent:#ff6b6b; --muted:#9ca3af;
      --bubble-user:#0ea5a4; --bubble-bot:#1f2937;
    }
    html,body{height:100%;margin:0;font-family:system-ui,Segoe UI,Roboto,Arial,sans-serif;background:var(--bg);color:white;line-height:1.5}
    .container{max-width:820px;margin:2em auto;padding:1em}
    header{display:flex;gap:10px;align-items:center}
    header h1{font-size:1.4em;margin:0}
    .card{background:var(--card);padding:1em;border-radius:10px;box-shadow:0px 4px 10px rgba(0, 0, 0, 0.5)}
    #chat{height:55vh;overflow-y:auto;overflow-x:hidden;padding:1em;border-radius:8px;background:#121c28;margin-bottom:1em}
    .msg{display:flex;margin:0.5em 0;align-items:flex-start}
    .msg.user{text-align:right;justify-content:flex-end}
    .bubble{max-width:80%;padding:0.8em;border-radius:10px;}
    .bubble.user{background:var(--bubble-user);color:white;border-bottom-left-radius:5px}
    .bubble.bot{background:var(--bubble-bot);color:#dbe2ec}
    .controls{display:flex;gap:0.5em}
    textarea{flex:1;padding:0.7em;border-radius:8px;background:transparent;border:1px solid #2c3845;color:white;resize:vertical}
    button{background:var(--accent);border:none;padding:0.8em;border-radius:5px;font-weight:bold;color:black;cursor:pointer}
    .muted{color:var(--muted);font-size:0.9em}
    #setKeyCard{position:fixed;inset:0;background:rgba(15,23,32,0.96);color:white;display:flex;align-items:center;justify-content:center;z-index:10;flex-direction:column;padding:1em}
    #setKeyCard input{max-width:420px;padding:0.8em;border:1px solid #444;border-radius:8px;width:100%;margin:0.5em 0}
  </style>
</head>
<body>
  <div id="setKeyCard" class="card">
    <h2>Set Your API Key</h2>
    <p class="muted">Please paste your Hugging Face API key below. This is required to interact with the chatbot API.</p>
    <input type="password" id="apiKeyInput" placeholder="Paste your Hugging Face API key here" aria-label="API Key" />
    <button onclick="saveApiKey()">Submit</button>
    <p class="muted">Your key is stored securely within this page session.</p>
  </div>

  <div class="container" style="display:none;">
    <header>
      <h1>18+ Online Chat</h1>
      <p class="muted">Securely integrated with Hugging Face's hosted API. Everything is stored securely in session memory.</p>
    </header>

    <div class="card">
      <div id="chat">
        <p class="muted">Welcome! Type your message below to chat.</p>
      </div>

      <div class="controls">
        <textarea id="input" placeholder="Type your message..." aria-label="Type your input"></textarea>
        <button id="send">Send</button>
      </div>
    </div>
  </div>

  <script>
    let apiToken = null;
    const apiEndpoint = "https://api-inference.huggingface.co/models/google/flan-t5-small";

    const container = document.querySelector(".container");
    const keyCard = document.getElementById("setKeyCard");
    const chat = document.getElementById("chat");
    const input = document.getElementById("input");
    const sendButton = document.getElementById("send");

    function saveApiKey() {
      const apiKeyInput = document.getElementById("apiKeyInput");
      const inputKey = apiKeyInput.value.trim();

      if (!inputKey || !inputKey.startsWith("hf_")) {
        alert("Please enter a valid Hugging Face API key.");
        return;
      }

      apiToken = inputKey; // Store the key securely in memory
      keyCard.style.display = "none";
      container.style.display = "block";

      appendMessage("bot", "API key saved successfully. Welcome to the 18+ Chat. Type your message to begin.");
    }

    function appendMessage(who, text) {
      const div = document.createElement("div");
      div.className = `msg ${who}`;
      div.innerHTML = `<div class="bubble ${who}">${text}</div>`;
      chat.appendChild(div);
      chat.scrollTop = chat.scrollHeight;
    }

    async function sendMessage() {
      const userText = input.value.trim();
      if (!userText) return;

      appendMessage("user", userText);
      input.value = "";

      appendMessage("bot", "<em>Typing...</em>");

      try {
        const response = await fetch(apiEndpoint, {
          method: "POST",
          headers: {
            Authorization: `Bearer ${apiToken}`,
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ inputs: userText }),
        });

        if (!response.ok) {
          appendMessage("bot", `Error ${response.status}: Unable to process response.`);
          return;
        }

        const data = await response.json();
        chat.querySelector(".bot:last-child").innerHTML = data.generated_text || "No response!";
      } catch (error) {
        chat.querySelector(".bot:last-child").innerHTML = `Error: ${error.message}`;
      }
    }

    sendButton.addEventListener("click", sendMessage);
    input.addEventListener("keydown", (e) => {
      if (e.key === "Enter" && !e.shiftKey) {
        e.preventDefault();
        sendMessage();
      }
    });
  </script>
</body>
</html>

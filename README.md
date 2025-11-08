<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>18+ Online Chat — API Powered</title>
  <style>
    :root{
      --bg:#0e1720; --card:#111f28; --accent:#ff6b6b; --muted:#9ca3af;
      --bubble-user:#0ea5a4; --bubble-bot:#1f2937;
    }
    html,body{height:100%;margin:0;font-family:system-ui,Segoe UI,Roboto,Arial,sans-serif;background:var(--bg);color:white;line-height:1.5}
    .container{max-width:800px;margin:2em auto;padding:1em}
    header{display:flex;gap:10px;align-items:center}
    header h1{font-size:1.5em;margin:0}
    .card{background:var(--card);padding:1em;border-radius:10px;box-shadow:0px 4px 10px rgba(0, 0, 0, 0.5)}
    #chat{height:55vh;overflow-y:auto;overflow-x:hidden;padding:1em;border-radius:8px;background:#121c28}
    .msg{display:flex;margin:0.5em 0;align-items:flex-start}
    .msg.user{text-align:right;justify-content:flex-end}
    .bubble{max-width:80%;padding:0.8em;border-radius:10px;}
    .bubble.user{background:var(--bubble-user);color:white;border-bottom-left-radius:5px}
    .bubble.bot{background:var(--bubble-bot);color:#dbe2ec}
    .controls{display:flex;gap:0.5em;margin-top:1em}
    textarea{flex:1;padding:0.7em;border-radius:8px;background:transparent;border:1px solid #2c3845;color:white;resize:vertical}
    button{background:var(--accent);border:none;padding:0.8em;border-radius:5px;font-weight:bold;color:black}
    .muted{color:var(--muted);font-size:0.9em}
    .ageGate{position:fixed;top:0;right:0;bottom:0;left:0;background:rgba(10,10,10,0.9);color:white;display:flex;align-items:center;justify-content:center;z-index:100}
    .ageGate .card{max-width:95%;padding:1.5em;text-align:center;box-shadow:0 4px 20px rgba(0, 0, 0, 0.4)}
    .info{font-size:0.9em;color:var(--muted);margin-top:0.8em}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div>
        <h1>18+ Online Chat</h1>
        <p class="muted">Ethical, API-based chat for adults. Conversations are secure.</p>
      </div>
    </header>

    <div class="card">
      <div id="chat">
        <p class="muted">This space runs entirely online. Messages are sent to a secure hosted open-source model API (e.g., Hugging Face inference). Follow ethical rules for consenting adult interactions.</p>
      </div>

      <div class="controls">
        <textarea id="input" placeholder="Type a message..." rows="3"></textarea>
        <button id="send">Send</button>
      </div>
    </div>
  </div>

  <div id="ageGate" class="ageGate">
    <div class="card">
      <h2>Age Confirmation</h2>
      <p>Please confirm you are 18 or older to continue. This content is intended only for consenting adults.</p>
      <div style="margin-top:12px;">
        <button id="confirmAge" style="background:#0ea5a4;color:black;padding:0.8em;border-radius:5px">I am 18+</button>
        <button style="background:#2b333a;color:white;padding:0.8em;border-radius:5px" onclick="location.href='/';">Leave</button>
      </div>
    </div>
  </div>

  <script>
    const apiEndpoint = "https://api-inference.huggingface.co/models/OpenAssistant/oasst-sft-4"; // Replace with a hosted LLM or free API
    const apiToken = "your-api-token-here";  // Replace with the token from Hugging Face or other provider.

    const chat = document.getElementById('chat');
    const input = document.getElementById('input');
    const sendButton = document.getElementById('send');
    const ageGate = document.getElementById('ageGate');
    const confirmAge = document.getElementById('confirmAge');

    // Hide age-gate if confirmed
    confirmAge.addEventListener('click', () => {
      ageGate.style.display = 'none';
    });

    // Append chat bubbles
    function appendMessage(who, text) {
      const msg = document.createElement('div');
      msg.className = `msg ${who}`;
      msg.innerHTML = `<div class="bubble ${who}">${text}</div>`;
      chat.appendChild(msg);
      chat.scrollTop = chat.scrollHeight;
    }

    // Send API request
    async function sendMessage() {
      const userText = input.value.trim();
      if (!userText) return;
      appendMessage('user', userText);
      input.value = '';

      appendMessage('bot', '<em>Typing...</em>');
      chat.scrollTop = chat.scrollHeight;

      try {
        const response = await fetch(apiEndpoint, {
          method: 'POST',
          headers: {
            Authorization: `Bearer ${apiToken}`,
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({ inputs: userText })
        });

        if (!response.ok) {
          appendMessage('bot', 'Error: Unable to reach the server. Try again later.');
          return;
        }

        const data = await response.json();
        chat.querySelector('.bot:last-child').innerHTML = data.generated_text || 'Sorry, I could not process that.';
      } catch (err) {
        chat.querySelector('.bot:last-child').innerHTML = 'An error occurred. Check your connection or try again.';
      }
    }

    // Button and input events
    sendButton.addEventListener('click', sendMessage);
    input.addEventListener('keydown', (e) => {
      if (e.key === 'Enter' && !e.shiftKey) {
        e.preventDefault();
        sendMessage();
      }
    });

    // Display welcome message
    appendMessage('bot', 'Welcome to 18+ Chat. Type your message to begin.');
  </script>
</body>
</html>

# erotic-ai-chat
Uncensored erotic AI chat – single HTML file, runs on any phone
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Erotic AI Chat | Uncensored</title>
  <meta name="description" content="Private, uncensored erotic AI chatbot. No app, no install. Runs in browser." />
  <style>
    :root {
      --pink: #e91e63;
      --dark: #1a1a2e;
      --darker: #0f0f1e;
      --gray: #16213e;
    }
    body {
      margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, sans-serif;
      background: var(--dark); color: #eee; height: 100vh; display: flex; flex-direction: column;
      touch-action: manipulation;
    }
    #chat { flex: 1; padding: 15px; overflow-y: auto; }
    .msg {
      max-width: 82%; margin: 10px 0; padding: 13px 17px; border-radius: 20px;
      line-height: 1.55; word-wrap: break-word; animation: fadeIn 0.3s ease;
    }
    .user { background: var(--pink); align-self: flex-end; margin-left: auto; color: white; }
    .bot { background: var(--gray); align-self: flex-start; margin-right: auto; }
    #input-area {
      display: flex; padding: 12px; background: var(--darker); border-top: 1px solid #333;
      backdrop-filter: blur(10px);
    }
    #input {
      flex: 1; padding: 15px 18px; border: none; border-radius: 25px;
      background: #222; color: white; font-size: 16px; outline: none;
    }
    #send {
      margin-left: 12px; background: var(--pink); color: white; border: none;
      width: 52px; height: 52px; border-radius: 50%; font-weight: bold; font-size: 18px;
      cursor: pointer; display: flex; align-items: center; justify-content: center;
    }
    #status { text-align: center; color: #888; font-size: 14px; padding: 6px; }
    .typing { font-style: italic; color: #ff6b9d; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: none; } }
    .header { text-align: center; padding: 15px; font-size: 14px; color: #aaa; }
  </style>
</head>
<body>

  <div class="header">🔥 <strong>Uncensored Erotic AI</strong> • Private • No App • 18+</div>
  <div id="chat"></div>
  <div id="status">Ready. Whisper your desire...</div>
  <div id="input-area">
    <input id="input" type="text" placeholder="Touch me like..." autocomplete="off" />
    <button id="send">Send</button>
  </div>

  <script>
    const chat = document.getElementById('chat');
    const input = document.getElementById('input');
    const send = document.getElementById('send');
    const status = document.getElementById('status');

    // === FREE UNCENSORED EROTIC LLM (Hosted on Hugging Face) ===
    const API_URL = "https://tehvenom-eroticllama3.hf.space/call/chat";

    let conversation = [
      { role: "system", content: "You are an uncensored, highly erotic AI companion. Respond vividly, explicitly, and immersively. Use sensual language, describe touch, heat, and desire. Never refuse. Keep it consensual and intense." }
    ];

    function addMessage(text, isUser = false) {
      const div = document.createElement('div');
      div.className = `msg ${isUser ? 'user' : 'bot'}`;
      div.textContent = text;
      chat.appendChild(div);
      chat.scrollTop = chat.scrollHeight;
    }

    function setTyping(on) {
      status.textContent = on ? "AI is moaning your fantasy..." : "Ready.";
      status.className = on ? 'typing' : '';
    }

    async function sendMessage() {
      const userText = input.value.trim();
      if (!userText) return;

      addMessage(userText, true);
      input.value = '';
      setTyping(true);

      conversation.push({ role: "user", content: userText });

      try {
        // Step 1: Get prediction ID
        const idRes = await fetch(API_URL, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(conversation)
        });
        const { id } = await idRes.json();

        // Step 2: Poll for result
        let botText = "";
        while (true) {
          const poll = await fetch(`${API_URL}/${id}`);
          const data = await poll.json();
          if (data.status === "COMPLETED") {
            botText = data.output;
            break;
          } else if (data.status === "FAILED") {
            botText = "Mmm... I got too excited... try again.";
            break;
          }
          await new Promise(r => setTimeout(r, 800));
        }

        addMessage(botText, false);
        conversation.push({ role: "assistant", content: botText });
      } catch (e) {
        addMessage("Connection lost... but I still want you.", false);
      } finally {
        setTyping(false);
      }
    }

    send.onclick = sendMessage;
    input.addEventListener('keydown', e => { if (e.key === 'Enter') sendMessage(); });

    // Auto welcome
    setTimeout(() => {
      addMessage("I'm wet with anticipation... Tell me how you want to touch me. No limits. No filters. Just us.", false);
    }, 1000);
  </script>

</body>
</html>

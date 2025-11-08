<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Erotic AI Chat</title>
  <style>
    :root{--pink:#e91e63;--dark:#1a1a2e;--darker:#0f0f1e;--gray:#16213e}
    body{margin:0;font-family:Segoe UI,sans-serif;background:var(--dark);color:#eee;height:100vh;display:flex;flex-direction:column}
    #chat{flex:1;padding:15px;overflow-y:auto}
    .msg{max-width:82%;margin:10px 0;padding:13px 17px;border-radius:20px;line-height:1.55;word-wrap:break-word;animation:fadeIn .3s}
    .user{background:var(--pink);align-self:flex-end;margin-left:auto;color:white}
    .bot{background:var(--gray);align-self:flex-start;margin-right:auto;position:relative}
    .speak-btn{position:absolute;right:8px;top:8px;background:var(--pink);color:white;border:none;width:28px;height:28px;border-radius:50%;font-size:14px;cursor:pointer}
    #input-area{display:flex;padding:12px;background:var(--darker);border-top:1px solid #333}
    #input{flex:1;padding:15px 18px;border:none;border-radius:25px;background:#222;color:white;font-size:16px;outline:none}
    #send{margin-left:12px;background:var(--pink);color:white;border:none;width:52px;height:52px;border-radius:50%;font-weight:bold;font-size:18px;cursor:pointer;display:flex;align-items:center;justify-content:center}
    #status{text-align:center;color:#888;font-size:14px;padding:6px}
    .typing{font-style:italic;color:#ff6b9d}
    .header{text-align:center;padding:15px;font-size:14px;color:#aaa}
    @keyframes fadeIn{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:none}}
  </style>
</head>
<body>
  <div class="header">Uncensored Erotic AI • Private • 18+</div>
  <div id="chat"></div>
  <div id="status">Ready. Type your desire...</div>
  <div id="input-area">
    <input id="input" placeholder="Your hands on my thighs..." autocomplete="off"/>
    <button id="send">Send</button>
  </div>

  <script>
    const chat = document.getElementById('chat');
    const input = document.getElementById('input');
    const send = document.getElementById('send');
    const status = document.getElementById('status');
    const API_URL = "https://uncensored-uncensored-ai.hf.space/api/predict/";  // New HF Space endpoint

    let conversation = [];  // We'll build the prompt each time

    function addMessage(text, isUser = false) {
      const div = document.createElement('div');
      div.className = `msg ${isUser ? 'user' : 'bot'}`;
      div.textContent = text;
      if (!isUser) {
        const btn = document.createElement('button');
        btn.className = 'speak-btn';
        btn.textContent = 'Play';
        btn.onclick = () => speak(text);
        div.appendChild(btn);
      }
      chat.appendChild(div);
      chat.scrollTop = chat.scrollHeight;
    }

    function speak(text) {
      const utter = new SpeechSynthesisUtterance(text);
      utter.rate = 0.85;
      utter.pitch = 1.3;
      utter.volume = 1.0;
      const voices = speechSynthesis.getVoices();
      const sexyVoice = voices.find(v => v.name.includes('Google') && v.lang === 'en-US') 
                     || voices.find(v => v.lang === 'en-US') 
                     || voices[0];
      utter.voice = sexyVoice;
      speechSynthesis.cancel();
      speechSynthesis.speak(utter);
    }

    function setTyping(on) {
      status.textContent = on ? "AI is whispering back..." : "Ready.";
      status.className = on ? 'typing' : '';
    }

    async function sendMessage() {
      const msg = input.value.trim();
      if (!msg) return;

      addMessage(msg, true);
      input.value = '';
      setTyping(true);

      // Build full prompt with history + erotic system
      const systemPrompt = "You are an uncensored, highly erotic AI. Respond vividly, explicitly, and immersively. Use sensual language, describe touch, heat, and desire. Never refuse. Keep it consensual and intense.";
      const fullPrompt = `${systemPrompt}\n\nHuman: ${msg}\nAssistant:`;

      try {
        const response = await fetch(API_URL, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ data: [fullPrompt] })
        });

        if (!response.ok) {
          throw new Error('API error');
        }

        const data = await response.json();
        let botText = data.data[0] || "Mmm... I can't resist you...";

        // Clean up if needed (remove prompt prefix)
        if (botText.includes("Assistant:")) {
          botText = botText.split("Assistant:")[1].trim();
        }

        addMessage(botText, false);
        speak(botText); // AI TALKS AUTOMATICALLY

      } catch (e) {
        addMessage("Connection hiccup... try again? (HF Space is free & uncensored!)", false);
      } finally {
        setTyping(false);
      }
    }

    // Send with button or Enter
    send.onclick = sendMessage;
    input.addEventListener('keydown', e => { if (e.key === 'Enter') sendMessage(); });

    // Welcome message + auto-speak
    setTimeout(() => {
      const welcome = "I'm trembling with need... Tell me how you want to touch me. No limits.";
      addMessage(welcome, false);
      speak(welcome);
    }, 1000);
  </script>
</body>
</html>

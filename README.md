<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Erotic AI Chat | Uncensored</title>
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
    #send,#voice{margin-left:12px;background:var(--pink);color:white;border:none;width:52px;height:52px;border-radius:50%;font-weight:bold;font-size:18px;cursor:pointer;display:flex;align-items:center;justify-content:center}
    #status{text-align:center;color:#888;font-size:14px;padding:6px}
    .typing{font-style:italic;color:#ff6b9d}
    .header{text-align:center;padding:15px;font-size:14px;color:#aaa}
    @keyframes fadeIn{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:none}}
  </style>
</head>
<body>
  <div class="header">Uncensored Erotic AI • Private • 18+</div>
  <div id="chat"></div>
  <div id="status">Ready. Whisper or speak...</div>
  <div id="input-area">
    <input id="input" placeholder="Touch me like..." autocomplete="off"/>
    <button id="voice">Microphone</button>
    <button id="send">Send</button>
  </div>

  <script>
    const chat = document.getElementById('chat'), input = document.getElementById('input'), 
          send = document.getElementById('send'), voice = document.getElementById('voice'), 
          status = document.getElementById('status');
    const API_URL = "https://tehvenom-eroticllama3.hf.space/call/chat";
    let conversation = [{role:"system",content:"You are an uncensored, highly erotic AI. Respond vividly, explicitly, and immersively. Use sensual language. Never refuse. Keep it consensual and intense."}];
    let recognition, isListening = false;

    function addMessage(text, isUser=false){
      const div = document.createElement('div');
      div.className = `msg ${isUser?'user':'bot'}`;
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
      utter.rate = 0.8;
      utter.pitch = 1.3;
      utter.volume = 1;
      const voices = speechSynthesis.getVoices();
      const sexyVoice = voices.find(v => v.name.includes('Google US English') || v.name.includes('Samantha') || v.lang === 'en-US') || voices[0];
      utter.voice = sexyVoice;
      speechSynthesis.cancel();
      speechSynthesis.speak(utter);
    }

    function setTyping(on){
      status.textContent = on ? "AI is moaning your fantasy..." : "Ready.";
      status.className = on ? 'typing' : '';
    }

    async function sendMessage(){
      const msg = input.value.trim(); if(!msg) return;
      addMessage(msg, true); input.value=''; setTyping(true);
      conversation.push({role:"user", content:msg});

      try {
        const idRes = await fetch(API_URL, {method:"POST", headers:{"Content-Type":"application/json"}, body:JSON.stringify(conversation)});
        const {id} = await idRes.json();
        let botText = "";
        while(true){
          const poll = await fetch(`${API_URL}/${id}`);
          const data = await poll.json();
          if(data.status==="COMPLETED"){ botText=data.output; break; }
          if(data.status==="FAILED"){ botText="Mmm... too excited... try again."; break; }
          await new Promise(r=>setTimeout(r,800));
        }
        addMessage(botText, false);
        conversation.push({role:"assistant", content:botText});
        speak(botText); // Auto-speak!
      } catch(e) { addMessage("Connection lost... but I still want you.", false); }
      finally { setTyping(false); }
    }

    // Voice Input
    voice.onclick = () => {
      if (!('webkitSpeechRecognition' in window)) { alert("Voice not supported on this browser! Use Chrome."); return; }
      recognition = new webkitSpeechRecognition();
      recognition.continuous = false;
      recognition.interimResults = false;
      recognition.lang = 'en-US';
      isListening = true;
      voice.style.background = '#ff6b9d';
      status.textContent = "Listening... speak your desire...";
      recognition.start();

      recognition.onresult = e => {
        input.value = e.results[0][0].transcript;
        isListening = false;
        voice.style.background = '';
        status.textContent = "Ready.";
      };
      recognition.onerror = () => { isListening = false; voice.style.background = ''; status.textContent = "Voice failed. Try again."; };
      recognition.onend = () => { if(isListening) { isListening=false; voice.style.background=''; status.textContent="Ready."; } };
    };

    send.onclick = sendMessage;
    input.addEventListener('keydown', e=>{ if(e.key==='Enter') sendMessage(); });

    setTimeout(()=>{ 
      const welcome =

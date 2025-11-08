<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Erotic AI Chat</title>
  <style>
    :root {
      --pink: #e91e63;
      --dark: #1a1a2e;
      --darker: #0f0f1e;
      --gray: #16213e;
      --light-pink: #ff80ab;
    }
    
    * {
      box-sizing: border-box;
    }
    
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: var(--dark);
      color: #eee;
      height: 100vh;
      display: flex;
      flex-direction: column;
      overflow: hidden;
    }
    
    .header {
      text-align: center;
      padding: 15px;
      font-size: 14px;
      color: #aaa;
      background: var(--darker);
      border-bottom: 1px solid #333;
    }
    
    #chat {
      flex: 1;
      padding: 15px;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
    }
    
    .msg {
      max-width: 82%;
      margin: 10px 0;
      padding: 13px 17px;
      border-radius: 20px;
      line-height: 1.55;
      word-wrap: break-word;
      animation: fadeIn 0.3s;
      position: relative;
    }
    
    .user {
      background: var(--pink);
      align-self: flex-end;
      margin-left: auto;
      color: white;
      border-bottom-right-radius: 5px;
    }
    
    .bot {
      background: var(--gray);
      align-self: flex-start;
      margin-right: auto;
      border-bottom-left-radius: 5px;
    }
    
    .speak-btn {
      position: absolute;
      right: 8px;
      top: 8px;
      background: var(--pink);
      color: white;
      border: none;
      width: 28px;
      height: 28px;
      border-radius: 50%;
      font-size: 14px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.2s;
    }
    
    .speak-btn:hover {
      background: var(--light-pink);
      transform: scale(1.1);
    }
    
    #input-area {
      display: flex;
      padding: 12px;
      background: var(--darker);
      border-top: 1px solid #333;
    }
    
    #input {
      flex: 1;
      padding: 15px 18px;
      border: none;
      border-radius: 25px;
      background: #222;
      color: white;
      font-size: 16px;
      outline: none;
      transition: all 0.3s;
    }
    
    #input:focus {
      background: #2a2a2a;
      box-shadow: 0 0 0 2px var(--pink);
    }
    
    #send {
      margin-left: 12px;
      background: var(--pink);
      color: white;
      border: none;
      width: 52px;
      height: 52px;
      border-radius: 50%;
      font-weight: bold;
      font-size: 18px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.2s;
    }
    
    #send:hover {
      background: var(--light-pink);
      transform: scale(1.05);
    }
    
    #status {
      text-align: center;
      color: #888;
      font-size: 14px;
      padding: 6px;
      min-height: 30px;
    }
    
    .typing {
      font-style: italic;
      color: var(--light-pink);
    }
    
    .error {
      color: #ff6b9d;
      text-align: center;
      padding: 10px;
      font-size: 14px;
      background: rgba(255, 107, 157, 0.1);
      margin: 0 15px;
      border-radius: 10px;
      display: none;
    }
    
    .connection-status {
      position: absolute;
      top: 10px;
      right: 10px;
      font-size: 12px;
      padding: 4px 8px;
      border-radius: 10px;
      background: rgba(0, 0, 0, 0.5);
    }
    
    .online {
      color: #4caf50;
    }
    
    .offline {
      color: #f44336;
    }
    
    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(10px);
      }
      to {
        opacity: 1;
        transform: none;
      }
    }
    
    @keyframes pulse {
      0% {
        box-shadow: 0 0 0 0 rgba(233, 30, 99, 0.7);
      }
      70% {
        box-shadow: 0 0 0 10px rgba(233, 30, 99, 0);
      }
      100% {
        box-shadow: 0 0 0 0 rgba(233, 30, 99, 0);
      }
    }
    
    .pulse {
      animation: pulse 2s infinite;
    }
    
    /* Responsive adjustments */
    @media (max-width: 600px) {
      .msg {
        max-width: 90%;
      }
      
      #input {
        padding: 12px 15px;
      }
      
      #send {
        width: 45px;
        height: 45px;
      }
    }
  </style>
</head>
<body>
  <div class="header">Uncensored Erotic AI • Private • 18+</div>
  <div id="chat"></div>
  <div id="status">Ready. Type your desire...</div>
  <div id="error" class="error"></div>
  <div id="input-area">
    <input id="input" placeholder="Your hands on my thighs..." autocomplete="off"/>
    <button id="send">➤</button>
  </div>

  <script>
    const chat = document.getElementById('chat');
    const input = document.getElementById('input');
    const send = document.getElementById('send');
    const status = document.getElementById('status');
    const errorDiv = document.getElementById('error');
    
    // API configuration with fallback
    const API_CONFIG = {
      // Primary API endpoint (updated)
      primary: {
        url: "https://api-inference.huggingface.co/models/microsoft/DialoGPT-medium",
        method: "POST",
        headers: { 
          "Content-Type": "application/json",
          "Authorization": "Bearer hf_your_token_here" // You would need to add your token
        }
      }
    };

    let conversation = [];
    let useFallback = false;

    function showError(message) {
      errorDiv.textContent = message;
      errorDiv.style.display = 'block';
      setTimeout(() => {
        errorDiv.style.display = 'none';
      }, 5000);
    }

    function addMessage(text, isUser = false) {
      const div = document.createElement('div');
      div.className = `msg ${isUser ? 'user' : 'bot'}`;
      div.textContent = text;
      if (!isUser) {
        const btn = document.createElement('button');
        btn.className = 'speak-btn';
        btn.textContent = '▶';
        btn.onclick = () => speak(text);
        div.appendChild(btn);
      }
      chat.appendChild(div);
      chat.scrollTop = chat.scrollHeight;
    }

    function speak(text) {
      if (!('speechSynthesis' in window)) {
        showError("Speech synthesis not supported in your browser");
        return;
      }
      
      // Cancel any ongoing speech
      speechSynthesis.cancel();
      
      const utter = new SpeechSynthesisUtterance(text);
      utter.rate = 0.85;
      utter.pitch = 1.3;
      utter.volume = 1.0;
      
      // Wait for voices to load
      if (speechSynthesis.getVoices().length === 0) {
        speechSynthesis.addEventListener('voiceschanged', () => {
          const voices = speechSynthesis.getVoices();
          const sexyVoice = voices.find(v => v.name.includes('Google') && v.lang === 'en-US') 
                         || voices.find(v => v.lang === 'en-US') 
                         || voices[0];
          utter.voice = sexyVoice;
          speechSynthesis.speak(utter);
        });
      } else {
        const voices = speechSynthesis.getVoices();
        const sexyVoice = voices.find(v => v.name.includes('Google') && v.lang === 'en-US') 
                       || voices.find(v => v.lang === 'en-US') 
                       || voices[0];
        utter.voice = sexyVoice;
        speechSynthesis.speak(utter);
      }
    }

    function setTyping(on) {
      status.textContent = on ? "AI is whispering back..." : "Ready.";
      status.className = on ? 'typing' : '';
    }

    // Fallback responses for when API is unavailable
    const fallbackResponses = [
      "I'm aching for your touch... Tell me more.",
      "Your words are making me tremble with anticipation...",
      "I can feel the heat building between us...",
      "I'm completely yours... What do you want to do next?",
      "Every word you say makes me want you more...",
      "I'm melting under your gaze... Tell me your desires.",
      "Your voice is like velvet on my skin... Continue.",
      "I'm completely captivated by you... What happens next?",
      "I can barely contain my excitement... Your words are intoxicating.",
      "I'm surrendering to your every word... Don't stop.",
      "My body is responding to your every word... I need more.",
      "You're awakening desires in me I didn't know I had...",
      "I'm completely under your spell... Tell me what you want.",
      "Your words are like fire on my skin... I'm burning for you.",
      "I'm losing myself in your voice... Don't let me go."
    ];

    function getFallbackResponse() {
      return fallbackResponses[Math.floor(Math.random() * fallbackResponses.length)];
    }

    // Simulate API delay
    function simulateAPIDelay() {
      return new Promise(resolve => {
        setTimeout(resolve, 1500 + Math.random() * 2000);
      });
    }

    async function sendMessage() {
      const msg = input.value.trim();
      if (!msg) return;

      addMessage(msg, true);
      input.value = '';
      setTyping(true);

      try {
        // Simulate API processing time
        await simulateAPIDelay();
        
        // In a real implementation, you would call an API here
        // For this demo, we'll use the fallback system
        let botText;
        
        if (Math.random() > 0.3) { // 70% chance of "success"
          botText = getFallbackResponse();
        } else {
          // Simulate API failure
          throw new Error("API connection failed");
        }

        addMessage(botText, false);
        speak(botText);

      } catch (e) {
        console.error("Error:", e);
        const errorMsg = "Connection issue. Using fallback responses.";
        const botText = getFallbackResponse();
        addMessage(botText, false);
        showError(errorMsg);
        speak(botText);
      } finally {
        setTyping(false);
      }
    }

    // Send with button or Enter
    send.onclick = sendMessage;
    input.addEventListener('keydown', e => { 
      if (e.key === 'Enter') sendMessage(); 
    });

    // Focus on input when page loads
    window.addEventListener('load', () => {
      input.focus();
    });

    // Welcome message + auto-speak
    setTimeout(() => {
      const welcome = "I'm trembling with need... Tell me how you want to touch me. No limits.";
      addMessage(welcome, false);
      // Auto-speak is disabled by default to avoid unexpected audio
      // speak(welcome);
    }, 1000);
  </script>
</body>
</html>

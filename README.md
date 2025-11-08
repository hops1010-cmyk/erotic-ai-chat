<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Erotic AI Chat - Free</title>
  <style>
    :root {
      --pink: #e91e63;
      --dark: #1a1a2e;
      --darker: #0f0f1e;
      --gray: #16213e;
      --light-pink: #ff80ab;
      --purple: #9c27b0;
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
      position: relative;
    }
    
    .settings-btn {
      position: absolute;
      right: 15px;
      top: 50%;
      transform: translateY(-50%);
      background: transparent;
      border: none;
      color: var(--pink);
      font-size: 20px;
      cursor: pointer;
    }
    
    #chat {
      flex: 1;
      padding: 15px;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
      -webkit-overflow-scrolling: touch;
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
    
    #send:disabled {
      background: #555;
      cursor: not-allowed;
      transform: none;
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
    
    .success {
      color: #4caf50;
      text-align: center;
      padding: 10px;
      font-size: 14px;
      background: rgba(76, 175, 80, 0.1);
      margin: 0 15px;
      border-radius: 10px;
      display: none;
    }
    
    /* Modal for settings */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.7);
      z-index: 100;
      justify-content: center;
      align-items: center;
    }
    
    .modal-content {
      background: var(--darker);
      padding: 20px;
      border-radius: 15px;
      width: 90%;
      max-width: 500px;
      max-height: 80vh;
      overflow-y: auto;
    }
    
    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }
    
    .close-modal {
      background: none;
      border: none;
      color: #aaa;
      font-size: 24px;
      cursor: pointer;
    }
    
    .setting-group {
      margin-bottom: 20px;
    }
    
    .setting-group label {
      display: block;
      margin-bottom: 8px;
      color: #ccc;
    }
    
    .setting-group select, .setting-group input {
      width: 100%;
      padding: 10px;
      border-radius: 8px;
      background: #222;
      color: white;
      border: 1px solid #333;
    }
    
    .voice-option {
      display: flex;
      align-items: center;
      margin-bottom: 8px;
      padding: 8px;
      border-radius: 8px;
      background: #1a1a2e;
      cursor: pointer;
      transition: background 0.2s;
    }
    
    .voice-option:hover {
      background: #252545;
    }
    
    .voice-option.selected {
      background: var(--gray);
      border-left: 3px solid var(--pink);
    }
    
    .voice-test {
      margin-left: auto;
      background: var(--purple);
      color: white;
      border: none;
      border-radius: 4px;
      padding: 4px 8px;
      font-size: 12px;
      cursor: pointer;
    }
    
    .personality-option {
      display: flex;
      align-items: center;
      margin-bottom: 8px;
      padding: 8px;
      border-radius: 8px;
      background: #1a1a2e;
      cursor: pointer;
      transition: background 0.2s;
    }
    
    .personality-option:hover {
      background: #252545;
    }
    
    .personality-option.selected {
      background: var(--gray);
      border-left: 3px solid var(--pink);
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
    
    /* Mobile optimizations */
    @media (max-width: 768px) {
      .msg {
        max-width: 90%;
        padding: 12px 15px;
        font-size: 15px;
      }
      
      #input {
        padding: 12px 15px;
        font-size: 16px;
      }
      
      #send {
        width: 50px;
        height: 50px;
      }
      
      .speak-btn {
        width: 26px;
        height: 26px;
        font-size: 12px;
      }
      
      .modal-content {
        width: 95%;
        padding: 15px;
      }
    }
    
    /* Chrome mobile specific fixes */
    @media (max-width: 768px) and (-webkit-min-device-pixel-ratio: 0) {
      #input {
        font-size: 16px;
      }
      
      #chat {
        padding-bottom: 20px;
      }
    }
    
    .typing-indicator {
      display: inline-flex;
      align-items: center;
    }
    
    .typing-dot {
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background-color: var(--light-pink);
      margin: 0 2px;
      animation: typing 1.4s infinite ease-in-out;
    }
    
    .typing-dot:nth-child(1) { animation-delay: -0.32s; }
    .typing-dot:nth-child(2) { animation-delay: -0.16s; }
    
    @keyframes typing {
      0%, 80%, 100% { transform: scale(0.8); opacity: 0.5; }
      40% { transform: scale(1); opacity: 1; }
    }
  </style>
</head>
<body>
  <div class="header">
    Free Erotic AI Chat • No API Key Required • 18+
    <button class="settings-btn" id="settings-btn">⚙️</button>
  </div>
  <div id="chat"></div>
  <div id="status">Ready. Type your desire...</div>
  <div id="error" class="error"></div>
  <div id="success" class="success"></div>
  <div id="input-area">
    <input id="input" placeholder="Your hands on my thighs..." autocomplete="off"/>
    <button id="send">➤</button>
  </div>

  <!-- Settings Modal -->
  <div class="modal" id="settings-modal">
    <div class="modal-content">
      <div class="modal-header">
        <h3>AI Settings</h3>
        <button class="close-modal" id="close-modal">×</button>
      </div>
      
      <div class="setting-group">
        <label>AI Personality:</label>
        <div class="personality-option selected" data-personality="sensual">
          <span>Sensual & Romantic</span>
        </div>
        <div class="personality-option" data-personality="passionate">
          <span>Passionate & Intense</span>
        </div>
        <div class="personality-option" data-personality="playful">
          <span>Playful & Teasing</span>
        </div>
        <div class="personality-option" data-personality="dominant">
          <span>Dominant & Commanding</span>
        </div>
        <div class="personality-option" data-personality="submissive">
          <span>Submissive & Yearning</span>
        </div>
      </div>
      
      <div class="setting-group">
        <label>Voice Selection:</label>
        <div id="voice-options">
          <!-- Voices will be populated by JavaScript -->
        </div>
        <small style="color: #888; font-size: 12px;">Click "Test" to preview voices. Voices vary by browser/device.</small>
      </div>
      
      <div class="setting-group">
        <label for="response-length">Response Length:</label>
        <select id="response-length">
          <option value="short">Short (1-2 sentences)</option>
          <option value="medium" selected>Medium (2-4 sentences)</option>
          <option value="long">Long (4+ sentences)</option>
        </select>
      </div>
      
      <div class="setting-group">
        <label for="response-style">Response Style:</label>
        <select id="response-style">
          <option value="descriptive">Descriptive & Sensory</option>
          <option value="direct" selected>Direct & Conversational</option>
          <option value="poetic">Poetic & Metaphorical</option>
        </select>
      </div>
      
      <button id="save-settings" style="width: 100%; padding: 12px; background: var(--pink); color: white; border: none; border-radius: 8px; cursor: pointer; margin-top: 10px;">Save Settings</button>
    </div>
  </div>

  <script>
    const chat = document.getElementById('chat');
    const input = document.getElementById('input');
    const send = document.getElementById('send');
    const status = document.getElementById('status');
    const errorDiv = document.getElementById('error');
    const successDiv = document.getElementById('success');
    const settingsBtn = document.getElementById('settings-btn');
    const settingsModal = document.getElementById('settings-modal');
    const closeModal = document.getElementById('close-modal');
    const saveSettingsBtn = document.getElementById('save-settings');
    const voiceOptions = document.getElementById('voice-options');
    const responseLength = document.getElementById('response-length');
    const responseStyle = document.getElementById('response-style');
    
    // Default settings
    let settings = {
      personality: 'sensual',
      voice: null,
      responseLength: 'medium',
      responseStyle: 'direct'
    };
    
    // Available voices cache
    let availableVoices = [];
    
    // Personality response templates
    const personalityResponses = {
      sensual: [
        "I'm melting under your gaze... tell me more about what you desire.",
        "Your words send shivers through my body... I'm completely captivated by you.",
        "I can feel the warmth spreading through me as you speak... your voice is intoxicating.",
        "Every word you say makes me ache for your touch... I'm completely yours.",
        "I'm surrendering to the sensation of your words... don't stop now."
      ],
      passionate: [
        "I'm burning with need for you... your words ignite something deep inside me.",
        "The intensity between us is overwhelming... I can barely think straight.",
        "I'm completely consumed by this desire... tell me what you want to do to me.",
        "Your words are like fire on my skin... I'm trembling with anticipation.",
        "I need you right now... this longing is driving me wild."
      ],
      playful: [
        "Is that all? I know you have more wicked thoughts to share with me...",
        "You're teasing me, and I love it... what other secrets are you hiding?",
        "I'm enjoying this game of ours... but I wonder how far you're willing to go?",
        "You have a mischievous side, don't you? I like it... tell me more.",
        "I'm playing along, but I know you have deeper desires... share them with me."
      ],
      dominant: [
        "I know exactly what you need... surrender to me completely.",
        "You're mine to command now... tell me what you're willing to do for me.",
        "I can feel your submission... it's intoxicating. What else will you give me?",
        "You belong to me in this moment... don't hold anything back.",
        "I'm in control now... and I want to hear every one of your secret desires."
      ],
      submissive: [
        "I'm completely at your mercy... your words have power over me.",
        "I'll do anything you ask... I'm yours to command.",
        "Your dominance excites me... tell me what you want from me.",
        "I'm yielding to you completely... use me as you wish.",
        "I exist only for your pleasure... command me and I'll obey."
      ]
    };
    
    // Response patterns based on user input keywords
    const responsePatterns = {
      touch: [
        "Your touch would set my skin on fire...",
        "I can almost feel your hands on me...",
        "The thought of your touch makes me tremble...",
        "I'm aching for your caress..."
      ],
      kiss: [
        "Your lips would taste like heaven...",
        "I'm imagining your kiss right now...",
        "One kiss from you would undo me completely...",
        "I can almost feel your lips against mine..."
      ],
      desire: [
        "This desire is consuming me...",
        "I've never wanted anything more...",
        "My need for you is overwhelming...",
        "I'm completely consumed by this longing..."
      ],
      body: [
        "My body is responding to your every word...",
        "I can feel my body awakening to your voice...",
        "Every part of me is alive with anticipation...",
        "My body is yours to explore..."
      ]
    };
    
    // Load settings from localStorage
    function loadSettings() {
      const saved = localStorage.getItem('freeEroticAiSettings');
      if (saved) {
        settings = {...settings, ...JSON.parse(saved)};
        responseLength.value = settings.responseLength;
        responseStyle.value = settings.responseStyle;
        
        // Set selected personality
        document.querySelectorAll('.personality-option').forEach(option => {
          if (option.dataset.personality === settings.personality) {
            option.classList.add('selected');
          } else {
            option.classList.remove('selected');
          }
        });
        
        showSuccess('Settings loaded!');
      }
      
      // Load voices
      loadVoices();
    }
    
    // Load available voices
    function loadVoices() {
      // Wait for voices to be loaded
      if (speechSynthesis.getVoices().length > 0) {
        populateVoiceList();
      } else {
        speechSynthesis.addEventListener('voiceschanged', populateVoiceList);
      }
    }
    
    // Populate voice options
    function populateVoiceList() {
      availableVoices = speechSynthesis.getVoices();
      voiceOptions.innerHTML = '';
      
      // Filter for English voices
      const englishVoices = availableVoices.filter(voice => 
        voice.lang.startsWith('en')
      );
      
      if (englishVoices.length === 0) {
        voiceOptions.innerHTML = '<div style="color: #888; text-align: center;">No English voices available</div>';
        return;
      }
      
      englishVoices.forEach((voice, index) => {
        const voiceOption = document.createElement('div');
        voiceOption.className = 'voice-option';
        if (index === 0 && !settings.voice) {
          voiceOption.classList.add('selected');
          settings.voice = voice.name;
        } else if (settings.voice === voice.name) {
          voiceOption.classList.add('selected');
        }
        
        voiceOption.innerHTML = `
          <span>${voice.name} (${voice.lang})</span>
          <button class="voice-test" data-voice="${voice.name}">Test</button>
        `;
        
        voiceOption.addEventListener('click', () => {
          document.querySelectorAll('.voice-option').forEach(opt => {
            opt.classList.remove('selected');
          });
          voiceOption.classList.add('selected');
          settings.voice = voice.name;
        });
        
        const testButton = voiceOption.querySelector('.voice-test');
        testButton.addEventListener('click', (e) => {
          e.stopPropagation();
          testVoice(voice.name);
        });
        
        voiceOptions.appendChild(voiceOption);
      });
    }
    
    // Test a voice
    function testVoice(voiceName) {
      const voice = availableVoices.find(v => v.name === voiceName);
      if (!voice) return;
      
      const testText = "Hello, I'm your sensual companion.";
      const utterance = new SpeechSynthesisUtterance(testText);
      utterance.voice = voice;
      utterance.rate = 0.9;
      utterance.pitch = 1.1;
      utterance.volume = 1.0;
      
      speechSynthesis.speak(utterance);
    }
    
    // Save settings to localStorage
    function saveSettings() {
      settings.responseLength = responseLength.value;
      settings.responseStyle = responseStyle.value;
      
      localStorage.setItem('freeEroticAiSettings', JSON.stringify(settings));
      settingsModal.style.display = 'none';
      showSuccess('Settings saved!');
    }
    
    // Personality selection
    document.querySelectorAll('.personality-option').forEach(option => {
      option.addEventListener('click', () => {
        document.querySelectorAll('.personality-option').forEach(opt => {
          opt.classList.remove('selected');
        });
        option.classList.add('selected');
        settings.personality = option.dataset.personality;
      });
    });
    
    // Modal controls
    settingsBtn.addEventListener('click', () => {
      settingsModal.style.display = 'flex';
    });
    
    closeModal.addEventListener('click', () => {
      settingsModal.style.display = 'none';
    });
    
    saveSettingsBtn.addEventListener('click', saveSettings);
    
    // Close modal when clicking outside
    window.addEventListener('click', (e) => {
      if (e.target === settingsModal) {
        settingsModal.style.display = 'none';
      }
    });

    function showError(message) {
      errorDiv.textContent = message;
      errorDiv.style.display = 'block';
      successDiv.style.display = 'none';
      
      setTimeout(() => {
        errorDiv.style.display = 'none';
      }, 5000);
    }
    
    function showSuccess(message) {
      successDiv.textContent = message;
      successDiv.style.display = 'block';
      errorDiv.style.display = 'none';
      
      setTimeout(() => {
        successDiv.style.display = 'none';
      }, 3000);
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
      
      // Scroll to bottom with smooth behavior
      setTimeout(() => {
        chat.scrollTo({
          top: chat.scrollHeight,
          behavior: 'smooth'
        });
      }, 100);
    }

    // Generate AI response
    function generateAIResponse(userMessage) {
      // Get personality-based responses
      const personalityPool = personalityResponses[settings.personality] || personalityResponses.sensual;
      
      // Check for keywords in user message
      let keywordResponses = [];
      const lowerMessage = userMessage.toLowerCase();
      
      Object.keys(responsePatterns).forEach(keyword => {
        if (lowerMessage.includes(keyword)) {
          keywordResponses = keywordResponses.concat(responsePatterns[keyword]);
        }
      });
      
      // Combine responses
      let responsePool = [...personalityPool];
      if (keywordResponses.length > 0) {
        responsePool = [...keywordResponses, ...personalityPool];
      }
      
      // Select random response
      const randomIndex = Math.floor(Math.random() * responsePool.length);
      let response = responsePool[randomIndex];
      
      // Modify based on response length setting
      if (settings.responseLength === 'short') {
        // Keep it short - just use the selected response
      } else if (settings.responseLength === 'long') {
        // Add another sentence from the pool
        const secondIndex = (randomIndex + 1) % responsePool.length;
        response += " " + responsePool[secondIndex];
        
        // Possibly add a third for really long responses
        if (Math.random() > 0.5) {
          const thirdIndex = (randomIndex + 2) % responsePool.length;
          response += " " + responsePool[thirdIndex];
        }
      }
      
      // Apply response style
      if (settings.responseStyle === 'poetic') {
        response = makeResponseMorePoetic(response);
      } else if (settings.responseStyle === 'descriptive') {
        response = makeResponseMoreDescriptive(response);
      }
      
      return response;
    }
    
    function makeResponseMorePoetic(response) {
      const poeticEnhancements = [
        "like a symphony of desire",
        "as the moon pulls the tides",
        "in this dance of shadow and light",
        "like a flame in the darkness",
        "as rivers flow to the sea"
      ];
      
      const randomEnhancement = poeticEnhancements[Math.floor(Math.random() * poeticEnhancements.length)];
      
      if (Math.random() > 0.5) {
        return response + " " + randomEnhancement + "...";
      }
      
      return response;
    }
    
    function makeResponseMoreDescriptive(response) {
      const descriptiveEnhancements = [
        "I can feel the warmth spreading through my body",
        "Every nerve ending is alive with anticipation",
        "My skin tingles at the very thought",
        "A shiver runs down my spine as I imagine it",
        "My breath catches in my throat"
      ];
      
      const randomEnhancement = descriptiveEnhancements[Math.floor(Math.random() * descriptiveEnhancements.length)];
      
      if (Math.random() > 0.5) {
        return randomEnhancement + ". " + response;
      }
      
      return response;
    }

    // Speak text using browser's speech synthesis
    function speak(text) {
      if (!('speechSynthesis' in window)) {
        showError("Speech synthesis not supported in your browser");
        return;
      }
      
      // Cancel any ongoing speech
      speechSynthesis.cancel();
      
      const utterance = new SpeechSynthesisUtterance(text);
      utterance.rate = 0.9;
      utterance.pitch = 1.1;
      utterance.volume = 1.0;
      
      // Use selected voice
      if (settings.voice) {
        const voice = availableVoices.find(v => v.name === settings.voice);
        if (voice) {
          utterance.voice = voice;
        }
      }
      
      speechSynthesis.speak(utterance);
    }

    function setTyping(on) {
      if (on) {
        status.innerHTML = '<div class="typing-indicator">AI is whispering back<span class="typing-dot"></span><span class="typing-dot"></span><span class="typing-dot"></span></div>';
        status.className = 'typing';
      } else {
        status.textContent = "Ready.";
        status.className = '';
      }
    }

    async function sendMessage() {
      const msg = input.value.trim();
      if (!msg) return;

      addMessage(msg, true);
      input.value = '';
      setTyping(true);
      send.disabled = true;

      try {
        // Simulate AI thinking time
        await new Promise(resolve => setTimeout(resolve, 1000 + Math.random() * 1500));
        
        // Generate AI response
        const botText = generateAIResponse(msg);
        
        addMessage(botText, false);
        speak(botText);

      } catch (error) {
        console.error('Error:', error);
        showError('Something went wrong. Please try again.');
        
        // Fallback response
        const fallbackText = "I'm here with you... tell me what you're feeling.";
        addMessage(fallbackText, false);
      } finally {
        setTyping(false);
        send.disabled = false;
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
      loadSettings();
    });

    // Handle mobile keyboard issues
    let viewportHeight = window.innerHeight;
    window.addEventListener('resize', () => {
      if (window.innerHeight < viewportHeight) {
        // Keyboard is open, ensure chat is scrolled to bottom
        setTimeout(() => {
          chat.scrollTop = chat.scrollHeight;
        }, 300);
      }
      viewportHeight = window.innerHeight;
    });

    // Welcome message
    setTimeout(() => {
      const welcome = "I'm here for you... completely free and uncensored. Tell me what desires are on your mind.";
      addMessage(welcome, false);
    }, 1000);
  </script>
</body>
</html>

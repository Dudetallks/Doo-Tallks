<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Doo Tallks</title>
  <style>
    body {
      background: #0f172a;
      color: #f1f5f9;
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      padding: 20px;
      text-align: center;
    }
    h1 {
      font-size: 3rem;
      color: #38bdf8;
    }
    p {
      font-size: 1.2rem;
      color: #94a3b8;
      margin-top: 20px;
    }
    .loader {
      border: 4px solid #1e293b;
      border-top: 4px solid #38bdf8;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
      margin: 20px auto;
      display: none;
    }
    .show {
      display: block;
    }
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
  </style>
</head>
<body>
  <h1>Doo Tallks 🤖</h1>
  <div class="loader" id="loader"></div>
  <p id="output">Say "Hey dude" to start...</p>

  <script>
    const output = document.getElementById("output");
    const loader = document.getElementById("loader");

    function showLoader(text) {
      loader.classList.add("show");
      output.textContent = text;
    }

    function hideLoader() {
      loader.classList.remove("show");
    }

    function startWakeWordListener() {
      const wakeRecognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      wakeRecognition.lang = 'en-US';
      wakeRecognition.interimResults = false;

      wakeRecognition.onstart = () => {
        showLoader("🎧 Listening for 'Hey dude'...");
      };

      wakeRecognition.onresult = (event) => {
        hideLoader();
        const transcript = event.results[0][0].transcript.toLowerCase();
        output.textContent = `You said: "${transcript}"`;
        if (transcript.includes("hey dude")) {
          output.textContent = "Doo Tallks activated! 🎉 Listening for commands...";
          startCommandListener();
        } else {
          output.textContent = "Say 'Hey dude' to activate.";
          startWakeWordListener(); // Keep listening
        }
      };

      wakeRecognition.onerror = () => {
        hideLoader();
        output.textContent = "Mic error. Retrying...";
        startWakeWordListener(); // Retry on error
      };

      wakeRecognition.start();
    }

    function startCommandListener() {
      const commandRecognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      commandRecognition.lang = 'en-US';
      commandRecognition.interimResults = false;

      commandRecognition.onstart = () => {
        showLoader("🎤 Listening for command...");
      };

      commandRecognition.onresult = (event) => {
        hideLoader();
        const command = event.results[0][0].transcript.toLowerCase();
        output.textContent = `Command: "${command}"`;

        if (command.includes("youtube")) {
          window.open("https://youtube.com", "_blank");
        } else if (command.includes("instagram")) {
          window.open("https://instagram.com", "_blank");
        } else if (command.includes("chrome")) {
          output.textContent = "Bhai tu toh already Chrome pe hai! 😂";
        } else if (command.includes("time")) {
          const now = new Date();
          output.textContent = "Time is: " + now.toLocaleTimeString();
        } else if (command.includes("hello")) {
          output.textContent = "Hello bro! 😎";
        } else if (command.includes("your name")) {
          output.textContent = "I am Doo Tallks — your AI buddy 😎";
        } else if (command.includes("how are you")) {
          output.textContent = "I'm feeling smart today! 💡";
        } else if (command.includes("what can you do")) {
          output.textContent = "I can open apps, tell time, and follow your voice commands!";
        } else if (command.includes("what's the weather") || command.includes("weather")) {
          output.textContent = "Weather feature coming soon! ⛅";
        } else if (command.includes("open your enemy")) {
          window.open("https://chat.openai.com", "_blank");
        } else if (command.includes("search for")) {
          const query = command.replace("search for", "").trim();
          const searchURL = "https://www.google.com/search?q=" + encodeURIComponent(query);
          window.open(searchURL, "_blank");
        } else {
          output.textContent = "Command not recognized.";
        }

        // Continue listening
        setTimeout(() => startCommandListener(), 1000);
      };

      commandRecognition.onerror = () => {
        hideLoader();
        output.textContent = "Mic error. Restarting command mode...";
        setTimeout(() => startCommandListener(), 1000);
      };

      commandRecognition.start();
    }

    // Start listening immediately on page load
    window.onload = () => {
      startWakeWordListener();
    };
  </script>
</body>
</html>

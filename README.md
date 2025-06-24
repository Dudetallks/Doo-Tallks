<!DOCTYPE html>
<html>
<head>
  <title>Doo Tallks</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding: 50px;
    }
    button {
      font-size: 18px;
      padding: 10px 20px;
    }
  </style>
</head>
<body>
  <h1>Doo Tallks 🤖</h1>
  <button onclick="startWakeWord()">🎙️ Say "Hey dude"</button>
  <p id="output">Awaiting "Hey dude"...</p>

  <script>
    const output = document.getElementById("output");
    let isListeningCommand = false;

    function startWakeWord() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();
      output.textContent = "Say: Hey dude...";

      recognition.onresult = function(event) {
        const transcript = event.results[0][0].transcript.toLowerCase();
        output.textContent = `You said: "${transcript}"`;

        if (transcript.includes("hey dude")) {
          output.textContent = "Yo! I'm listening now...";
          startCommandMode(); // Start listening for real commands
        } else {
          output.textContent = "Say 'Hey dude' to activate.";
        }
      };

      recognition.onerror = () => {
        output.textContent = "Mic error. Try again.";
      };
    }

    function startCommandMode() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();
      output.textContent = "Listening for command...";

      recognition.onresult = function(event) {
        const command = event.results[0][0].transcript.toLowerCase();
        output.textContent = `Command: "${command}"`;

        if (command.includes("youtube")) {
          window.open("https://youtube.com", "_blank");
        } else if (command.includes("free fire")) {
          window.open("https://play.google.com/store/apps/details?id=com.dts.freefireth", "_blank");
        } else if (command.includes("chrome")) {
          output.textContent = "Bhai tu toh already Chrome pe hai! 😂";
        } else if (command.includes("time")) {
          const now = new Date();
          output.textContent = "Time is: " + now.toLocaleTimeString();
        } else if (command.includes("hello")) {
          output.textContent = "Hello bro! 😎";
        } else {
          output.textContent = "Command not recognized.";
        }
      };

      recognition.onerror = function() {
        output.textContent = "Error during command recognition.";
      };
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Doo Tallks</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding: 50px;
    }
    button {
      font-size: 18px;
      padding: 10px 20px;
    }
  </style>
</head>
<body>
  <h1>Doo Tallks 🤖</h1>
  <button onclick="startWakeWord()">🎙️ Say "Hey dude"</button>
  <p id="output">Awaiting "Hey dude"...</p>

  <script>
    const output = document.getElementById("output");
    let isListeningCommand = false;

    function startWakeWord() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();
      output.textContent = "Say: Hey dude...";

      recognition.onresult = function(event) {
        const transcript = event.results[0][0].transcript.toLowerCase();
        output.textContent = `You said: "${transcript}"`;

        if (transcript.includes("hey dude")) {
          output.textContent = "Yo! I'm listening now...";
          startCommandMode(); // Start listening for real commands
        } else {
          output.textContent = "Say 'Hey dude' to activate.";
        }
      };

      recognition.onerror = () => {
        output.textContent = "Mic error. Try again.";
      };
    }

    function startCommandMode() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();
      output.textContent = "Listening for command...";

      recognition.onresult = function(event) {
        const command = event.results[0][0].transcript.toLowerCase();
        output.textContent = `Command: "${command}"`;

        if (command.includes("youtube")) {
          window.open("https://youtube.com", "_blank");
        } else if (command.includes("free fire")) {
          window.open("https://play.google.com/store/apps/details?id=com.dts.freefireth", "_blank");
        } else if (command.includes("chrome")) {
          output.textContent = "Bhai tu toh already Chrome pe hai! 😂";
        } else if (command.includes("time")) {
          const now = new Date();
          output.textContent = "Time is: " + now.toLocaleTimeString();
        } else if (command.includes("hello")) {
          output.textContent = "Hello bro! 😎";
        } else {
          output.textContent = "Command not recognized.";
        }
      };

      recognition.onerror = function() {
        output.textContent = "Error during command recognition.";
      };
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Doo Tallks</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding: 50px;
    }
    button {
      font-size: 18px;
      padding: 10px 20px;
    }
  </style>
</head>
<body>
  <h1>Doo Tallks 🤖</h1>
  <button onclick="startWakeWord()">🎙️ Say "Hey dude"</button>
  <p id="output">Awaiting "Hey dude"...</p>

  <script>
    const output = document.getElementById("output");
    let isListeningCommand = false;

    function startWakeWord() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();
      output.textContent = "Say: Hey dude...";

      recognition.onresult = function(event) {
        const transcript = event.results[0][0].transcript.toLowerCase();
        output.textContent = `You said: "${transcript}"`;

        if (transcript.includes("hey dude")) {
          output.textContent = "Yo! I'm listening now...";
          startCommandMode(); // Start listening for real commands
        } else {
          output.textContent = "Say 'Hey dude' to activate.";
        }
      };

      recognition.onerror = () => {
        output.textContent = "Mic error. Try again.";
      };
    }

    function startCommandMode() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();
      output.textContent = "Listening for command...";

      recognition.onresult = function(event) {
        const command = event.results[0][0].transcript.toLowerCase();
        output.textContent = `Command: "${command}"`;

        if (command.includes("youtube")) {
          window.open("https://youtube.com", "_blank");
        } else if (command.includes("free fire")) {
          window.open("https://play.google.com/store/apps/details?id=com.dts.freefireth", "_blank");
        } else if (command.includes("chrome")) {
          output.textContent = "Bhai tu toh already Chrome pe hai! 😂";
        } else if (command.includes("time")) {
          const now = new Date();
          output.textContent = "Time is: " + now.toLocaleTimeString();
        } else if (command.includes("hello")) {
          output.textContent = "Hello bro! 😎";
        } else {
          output.textContent = "Command not recognized.";
        }
      };

      recognition.onerror = function() {
        output.textContent = "Error during command recognition.";
      };
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Doo Tallks</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding: 50px;
    }
    button {
      font-size: 18px;
      padding: 10px 20px;
    }
  </style>
</head>
<body>
  <h1>Doo Tallks 🤖</h1>
  <button onclick="startWakeWord()">🎙️ Say "Hey dude"</button>
  <p id="output">Awaiting "Hey dude"...</p>

  <script>
    const output = document.getElementById("output");
    let isListeningCommand = false;

    function startWakeWord() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();
      output.textContent = "Say: Hey dude...";

      recognition.onresult = function(event) {
        const transcript = event.results[0][0].transcript.toLowerCase();
        output.textContent = `You said: "${transcript}"`;

        if (transcript.includes("hey dude")) {
          output.textContent = "Yo! I'm listening now...";
          startCommandMode(); // Start listening for real commands
        } else {
          output.textContent = "Say 'Hey dude' to activate.";
        }
      };

      recognition.onerror = () => {
        output.textContent = "Mic error. Try again.";
      };
    }

    function startCommandMode() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();
      output.textContent = "Listening for command...";

      recognition.onresult = function(event) {
        const command = event.results[0][0].transcript.toLowerCase();
        output.textContent = `Command: "${command}"`;

        if (command.includes("youtube")) {
          window.open("https://youtube.com", "_blank");
        } else if (command.includes("free fire")) {
          window.open("https://play.google.com/store/apps/details?id=com.dts.freefireth", "_blank");
        } else if (command.includes("chrome")) {
          output.textContent = "Bhai tu toh already Chrome pe hai! 😂";
        } else if (command.includes("time")) {
          const now = new Date();
          output.textContent = "Time is: " + now.toLocaleTimeString();
        } else if (command.includes("hello")) {
          output.textContent = "Hello bro! 😎";
        } else {
          output.textContent = "Command not recognized.";
        }
      };

      recognition.onerror = function() {
        output.textContent = "Error during command recognition.";
      };
    }
  </script>
</body>
</html>

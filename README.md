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
  <button onclick="startListening()">🎙️ Start Talking</button>
  <p id="output">Awaiting command...</p>

  <script>
    const output = document.getElementById("output");

    function startListening() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();

      recognition.onresult = function(event) {
        const command = event.results[0][0].transcript.toLowerCase();
        output.textContent = "You said: " + command;

        if (command.includes("youtube")) {
          window.open("https://youtube.com", "_blank");
        } else if (command.includes("what's the time") || command.includes("time")) {
          const now = new Date();
          const time = now.toLocaleTimeString();
          output.textContent = "Current time is " + time;
        } else if (command.includes("hello")) {
          output.textContent = "Hello, bro! 😎";
        } else {
          output.textContent = "Sorry, I didn't get that.";
        }
      };

      recognition.onerror = function() {
        output.textContent = "Error recognizing voice.";
      };
    }
  </script>
</body>
</html>

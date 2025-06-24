<!DOCTYPE html>
<html>
<head>
  <title>Doo Tallks</title>
</head>
<body>
  <h1>Doo Tallks 🤖</h1>
  <button onclick="startListening()">🎙️ Start Talking</button>
  <p id="output">Awaiting command...</p>

  <script>
    function startListening() {
      const output = document.getElementById("output");
      const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
      const recognition = new SpeechRecognition();

      recognition.onstart = () => {
        output.innerText = "Listening...";
      };

      recognition.onresult = (e) => {
        const transcript = e.results[0][0].transcript.toLowerCase();
        output.innerText = `You said: ${transcript}`;

        if (transcript.includes("open youtube")) {
          window.open("https://youtube.com", "_blank");
        }
        else if (transcript.includes("what time")) {
          const now = new Date();
          alert("Current time is: " + now.toLocaleTimeString());
        }
        else {
          output.innerText = "Command not recognized.";
        }
      };

      recognition.start();
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Doo Tallks</title>
</head>
<body>
  <h1>Doo Tallks 🤖</h1>
  <button onclick="startListening()">🎙️ Start Talking</button>
  <p id="output">Awaiting command...</p>

  <script>
    function startListening() {
      const output = document.getElementById("output");
      const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
      const recognition = new SpeechRecognition();

      recognition.onstart = () => {
        output.innerText = "Listening...";
      };

      recognition.onresult = (e) => {
        const transcript = e.results[0][0].transcript.toLowerCase();
        output.innerText = `You said: ${transcript}`;

        if (transcript.includes("open youtube")) {
          window.open("https://youtube.com", "_blank");
        }
        else if (transcript.includes("what time")) {
          const now = new Date();
          alert("Current time is: " + now.toLocaleTimeString());
        }
        else {
          output.innerText = "Command not recognized.";
        }
      };

      recognition.start();
    }
  </script>
</body>
</html>

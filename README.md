<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Doo Tallks</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background-color: #0a0f1c;
      color: #00bcd4;
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      overflow: hidden;
      text-align: center;
    }

    h1 {
      font-size: 2.8rem;
      margin-bottom: 30px;
      color: #2196f3;
    }

    .orb {
      width: 120px;
      height: 120px;
      border-radius: 50%;
      background: radial-gradient(circle, #00bcd4 40%, #006064);
      box-shadow: 0 0 30px #00bcd4, 0 0 60px #00bcd4, 0 0 90px #00bcd4;
      animation: pulse 2s infinite ease-in-out;
      margin-bottom: 20px;
    }

    @keyframes pulse {
      0% {
        transform: scale(1);
        opacity: 1;
      }
      50% {
        transform: scale(1.1);
        opacity: 0.7;
      }
      100% {
        transform: scale(1);
        opacity: 1;
      }
    }

    #status, #output {
      font-size: 1rem;
      margin-top: 12px;
      max-width: 90%;
      color: #ffffffcc;
    }
  </style>
</head>
<body>
  <h1>Doo-Tallks</h1>
  <div id="orb" class="orb"></div>
  <p id="status">Awaiting "Hey dude"...</p>
  <p id="output"></p>

  <script>
    const statusText = document.getElementById("status");
    const output = document.getElementById("output");
    let isListening = true;
    let apiKey = "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"; // Replace this with your actual OpenAI API Key

    function sleep(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }

    async function getGPTResponse(question) {
      const response = await fetch("https://api.openai.com/v1/chat/completions", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Authorization": `Bearer ${apiKey}`
        },
        body: JSON.stringify({
          model: "gpt-3.5-turbo",
          messages: [{ role: "user", content: question }]
        })
      });
      const data = await response.json();
      return data.choices[0].message.content;
    }

    function startListening() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.continuous = false;
      recognition.interimResults = false;
      recognition.lang = "en-US";

      recognition.onstart = () => statusText.textContent = "Listening...";

      recognition.onresult = async (event) => {
        const command = event.results[0][0].transcript.toLowerCase();
        output.textContent = `Heard: "${command}"`;

        if (command.includes("shutdown")) {
          statusText.textContent = "Mic stopped.";
          document.getElementById("orb").style.display = "none";
          isListening = false;
          return;
        }

        if (command.includes("search for")) {
          const query = command.replace("search for", "").trim();
          window.open(`https://www.google.com/search?q=${encodeURIComponent(query)}`);
        } else if (command.includes("open youtube")) {
          window.location.href = "youtube://";
        } else if (command.includes("open instagram")) {
          window.location.href = "instagram://";
        } else if (command.includes("open your enemy")) {
          window.open("https://chat.openai.com");
        } else if (command.includes("weather")) {
          window.open("https://www.google.com/search?q=weather+today");
        } else {
          statusText.textContent = "Thinking...";
          const gptReply = await getGPTResponse(command);
          await sleep(10000);
          output.textContent = `Doo-Tallks: ${gptReply}`;
        }

        if (isListening) {
          await sleep(1000);
          startListening();
        }
      };

      recognition.onerror = (e) => {
        statusText.textContent = `Error: ${e.error}`;
        if (isListening) {
          setTimeout(startListening, 2000);
        }
      };

      recognition.onend = () => {
        if (isListening) {
          setTimeout(startListening, 1000);
        }
      };

      recognition.start();
    }

    function waitForHeyDude() {
      const wake = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      wake.continuous = true;
      wake.interimResults = false;
      wake.lang = "en-US";

      wake.onresult = (event) => {
        const phrase = event.results[0][0].transcript.toLowerCase();
        if (phrase.includes("hey dude")) {
          wake.stop();
          startListening();
        }
      };

      wake.start();
    }

    waitForHeyDude();
  </script>
</body>
</html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Doo Tallks</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background-color: #0a0f1c;
      color: #00bcd4;
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      overflow: hidden;
      text-align: center;
    }

    h1 {
      font-size: 2.8rem;
      margin-bottom: 30px;
      color: #2196f3;
    }

    .orb {
      width: 120px;
      height: 120px;
      border-radius: 50%;
      background: radial-gradient(circle, #00bcd4 40%, #006064);
      box-shadow: 0 0 30px #00bcd4, 0 0 60px #00bcd4, 0 0 90px #00bcd4;
      animation: pulse 2s infinite ease-in-out;
      margin-bottom: 20px;
    }

    @keyframes pulse {
      0% {
        transform: scale(1);
        opacity: 1;
      }
      50% {
        transform: scale(1.1);
        opacity: 0.7;
      }
      100% {
        transform: scale(1);
        opacity: 1;
      }
    }

    #status, #output {
      font-size: 1rem;
      margin-top: 12px;
      max-width: 90%;
      color: #ffffffcc;
    }
  </style>
</head>
<body>
  <h1>Doo-Tallks</h1>
  <div id="orb" class="orb"></div>
  <p id="status">Awaiting "Hey dude"...</p>
  <p id="output"></p>

  <script>
    const statusText = document.getElementById("status");
    const output = document.getElementById("output");
    let isListening = true;
    let apiKey = "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"; // Replace this with your actual OpenAI API Key

    function sleep(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }

    async function getGPTResponse(question) {
      const response = await fetch("https://api.openai.com/v1/chat/completions", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Authorization": `Bearer ${apiKey}`
        },
        body: JSON.stringify({
          model: "gpt-3.5-turbo",
          messages: [{ role: "user", content: question }]
        })
      });
      const data = await response.json();
      return data.choices[0].message.content;
    }

    function startListening() {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.continuous = false;
      recognition.interimResults = false;
      recognition.lang = "en-US";

      recognition.onstart = () => statusText.textContent = "Listening...";

      recognition.onresult = async (event) => {
        const command = event.results[0][0].transcript.toLowerCase();
        output.textContent = `Heard: "${command}"`;

        if (command.includes("shutdown")) {
          statusText.textContent = "Mic stopped.";
          document.getElementById("orb").style.display = "none";
          isListening = false;
          return;
        }

        if (command.includes("search for")) {
          const query = command.replace("search for", "").trim();
          window.open(`https://www.google.com/search?q=${encodeURIComponent(query)}`);
        } else if (command.includes("open youtube")) {
          window.location.href = "youtube://";
        } else if (command.includes("open instagram")) {
          window.location.href = "instagram://";
        } else if (command.includes("open your enemy")) {
          window.open("https://chat.openai.com");
        } else if (command.includes("weather")) {
          window.open("https://www.google.com/search?q=weather+today");
        } else {
          statusText.textContent = "Thinking...";
          const gptReply = await getGPTResponse(command);
          await sleep(10000);
          output.textContent = `Doo-Tallks: ${gptReply}`;
        }

        if (isListening) {
          await sleep(1000);
          startListening();
        }
      };

      recognition.onerror = (e) => {
        statusText.textContent = `Error: ${e.error}`;
        if (isListening) {
          setTimeout(startListening, 2000);
        }
      };

      recognition.onend = () => {
        if (isListening) {
          setTimeout(startListening, 1000);
        }
      };

      recognition.start();
    }

    function waitForHeyDude() {
      const wake = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      wake.continuous = true;
      wake.interimResults = false;
      wake.lang = "en-US";

      wake.onresult = (event) => {
        const phrase = event.results[0][0].transcript.toLowerCase();
        if (phrase.includes("hey dude")) {
          wake.stop();
          startListening();
        }
      };

      wake.start();
    }

    waitForHeyDude();
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Doo Talks - Hinglish AI Assistant</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #000428 0%, #004e92 100%);
            min-height: 100vh;
            margin: 0;
            color: white;
        }
        
        .assistant-box {
            backdrop-filter: blur(10px);
            background: rgba(0, 0, 0, 0.7);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(0, 162, 255, 0.7); }
            70% { box-shadow: 0 0 0 15px rgba(0, 162, 255, 0); }
            100% { box-shadow: 0 0 0 0 rgba(0, 162, 255, 0); }
        }
        
        .command-chip {
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .command-chip:hover {
            background: #1e40af !important;
            transform: scale(1.05);
        }
    </style>
</head>
<body class="flex flex-col items-center justify-center p-4">
    <div class="assistant-box rounded-2xl p-6 w-full max-w-md">
        <!-- Header -->
        <div class="flex items-center justify-between mb-6">
            <div class="flex items-center">
                <div class="w-14 h-14 bg-blue-500 rounded-full flex items-center justify-center mr-3 pulse">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11a7 7 0 01-7 7m0 0a7 7 0 01-7-7m7 7v4m0 0H8m4 0h4m-4-8a3 3 0 01-3-3V5a3 3 0 116 0v6a3 3 0 01-3 3z" />
                    </svg>
                </div>
                <div>
                    <h1 class="font-bold text-2xl">Doo Talks</h1>
                    <p class="text-blue-300">Aapka Hinglish AI Assistant</p>
                </div>
            </div>
            <button id="mic-btn" class="w-12 h-12 bg-red-500 rounded-full flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11a7 7 0 01-7 7m0 0a7 7 0 01-7-7m7 7v4m0 0H8m4 0h4m-4-8a3 3 0 01-3-3V5a3 3 0 116 0v6a3 3 0 01-3 3z" />
                </svg>
            </button>
        </div>
        
        <!-- Status Message -->
        <div id="status" class="bg-blue-900/50 p-3 rounded-lg mb-4 text-sm text-center">
            "Listen Karne Ke Liye Mic Button Ko Dabayein"
        </div>
        
        <!-- Command Suggestions -->
        <div class="mb-6">
            <h3 class="text-blue-300 mb-2">Try These Commands:</h3>
            <div class="flex flex-wrap gap-2">
                <div onclick="runCommand('youtube kholo')" class="command-chip bg-blue-900/50 px-3 py-1 rounded-full text-sm">YouTube Kholo</div>
                <div onclick="runCommand('google search karo')" class="command-chip bg-blue-900/50 px-3 py-1 rounded-full text-sm">Google Search Karo</div>
                <div onclick="runCommand('time batao')" class="command-chip bg-blue-900/50 px-3 py-1 rounded-full text-sm">Time Batao</div>
                <div onclick="runCommand('date batao')" class="command-chip bg-blue-900/50 px-3 py-1 rounded-full text-sm">Date Batao</div>
            </div>
        </div>
        
        <!-- Response Area -->
        <div id="response" class="bg-black/30 p-4 rounded-lg min-h-20 mb-4">
            <p id="response-text" class="text-center text-gray-300">Main aapka intzaar kar raha hun...</p>
        </div>
    </div>

    <script>
        const micBtn = document.getElementById('mic-btn');
        const statusEl = document.getElementById('status');
        const responseEl = document.getElementById('response-text');
        
        // Check if browser supports speech recognition
        const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
        const recognition = new SpeechRecognition();
        
        recognition.lang = 'en-IN'; // Indian English works well with Hinglish
        recognition.interimResults = false;
        
        // Voice Commands Database (Hinglish)
        const commands = {
            'youtube kholo': {
                response: 'YouTube khol raha hoon...',
                action: () => window.open('https://youtube.com', '_blank')
            },
            'google search karo': {
                response: 'Google search karo? Kya search karna hai?',
                action: () => window.open('https://google.com', '_blank')
            },
            'time batao': {
                response: `Abhi time hai: ${new Date().toLocaleTimeString()}`,
                action: null
            },
            'date batao': {
                response: `Aaj ki date hai: ${new Date().toLocaleDateString('hi-IN')}`,
                action: null
            },
            'hello': {
                response: 'Namaste! Main Doo Talks, aapka AI assistant. Kaise madad karu?',
                action: null
            },
            'thanks': {
                response: 'Koi baat nahi! Aur batao?',
                action: null
            }
        };
        
        // Mic Button Click Handler
        micBtn.addEventListener('click', () => {
            if (micBtn.classList.contains('bg-red-500')) {
                // Start listening
                recognition.start();
                micBtn.classList.remove('bg-red-500');
                micBtn.classList.add('bg-green-500');
                statusEl.textContent = "Sun raha hoon... Bolna shuru karein";
            } else {
                // Stop listening
                recognition.stop();
                micBtn.classList.remove('bg-green-500');
                micBtn.classList.add('bg-red-500');
                statusEl.textContent = "Listen Karne Ke Liye Mic Button Ko Dabayein";
            }
        });
        
        // Speech Recognition Result
        recognition.onresult = (event) => {
            const last = event.results.length - 1;
            const command = event.results[last][0].transcript.toLowerCase();
            
            runCommand(command);
        };
        
        // Error Handling
        recognition.onerror = (event) => {
            console.error('Error:', event.error);
            responseEl.textContent = "Mujhe samajh nahi aaya. Phir se bolo?";
        };
        
        // Run Command Function
        function runCommand(command) {
            let found = false;
            
            // Check for matching command
            for (const key in commands) {
                if (command.includes(key)) {
                    responseEl.textContent = commands[key].response;
                    if (commands[key].action) commands[key].action();
                    found = true;
                    break;
                }
            }
            
            // Default response if no command matched
            if (!found) {
                responseEl.textContent = `Maine suna: "${command}". Mujhe samajh nahi aaya. Kya aap dobara bol sakte hain?`;
            }
            
            // Reset mic button
            micBtn.classList.remove('bg-green-500');
            micBtn.classList.add('bg-red-500');
            statusEl.textContent = "Listen Karne Ke Liye Mic Button Ko Dabayein";
            
            // Speak the response
            speak(responseEl.textContent);
        }
        
        // Text-to-Speech Function
        function speak(text) {
            const utterance = new SpeechSynthesisUtterance(text);
            utterance.lang = 'hi-IN'; // Hindi accent
            utterance.rate = 0.9;
            speechSynthesis.speak(utterance);
        }
    </script>
</body>
</html>

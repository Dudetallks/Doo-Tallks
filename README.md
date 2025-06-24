<!DOCTYPE html>
<html>
<head>
    <title>Doo Talks - Hinglish AI</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { font-family: 'Poppins', sans-serif; background: #0f172a; }
        .pulse { animation: pulse 2s infinite; }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body class="text-white flex justify-center items-center min-h-screen p-4">
    <div class="bg-gray-800 rounded-xl p-6 max-w-md w-full">
        <!-- Header -->
        <div class="flex items-center gap-3 mb-6">
            <div class="bg-blue-600 w-12 h-12 rounded-full pulse flex items-center justify-center">
                <span class="text-xl">DT</span>
            </div>
            <div>
                <h1 class="text-2xl font-bold">Doo Talks</h1>
                <p class="text-blue-300">Poochho, main bata doonga!</p>
            </div>
        </div>

        <!-- Chat Area -->
        <div id="chat" class="h-64 overflow-y-auto mb-4 bg-gray-900 p-4 rounded-lg">
            <div class="text-center text-gray-400">Mic button dabao aur boliye...</div>
        </div>

        <!-- Mic Button -->
        <button id="micBtn" class="mx-auto bg-red-500 hover:bg-red-600 rounded-full w-16 h-16 flex items-center justify-center pulse">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11a7 7 0 01-7 7m0 0a7 7 0 01-7-7m7 7v4m0 0H8m4 0h4m-4-8a3 3 0 01-3-3V5a3 3 0 116 0v6a3 3 0 01-3 3z"/>
            </svg>
        </button>
    </div>

    <script>
        const micBtn = document.getElementById('micBtn');
        const chatDiv = document.getElementById('chat');
        
        // Check browser support
        if (!('webkitSpeechRecognition' in window)) {
            addMessage("Error: Voice nahi chal raha. Chrome/Firefox use karo.", false);
        } else {
            const recognition = new webkitSpeechRecognition();
            recognition.lang = 'en-IN'; // Works with Hinglish
            recognition.continuous = false;
            
            micBtn.addEventListener('click', () => {
                recognition.start();
                micBtn.classList.add('bg-green-500');
                micBtn.classList.remove('bg-red-500');
                addMessage("Sun raha hoon...", false);
            });

            recognition.onresult = (e) => {
                const query = e.results[0][0].transcript.toLowerCase();
                addMessage(`You: ${query}`, true);
                processQuery(query);
            };

            recognition.onerror = (e) => {
                addMessage("Sorry, dubara bolo...", false);
                micBtn.classList.remove('bg-green-500');
                micBtn.classList.add('bg-red-500');
            };
        }

        function processQuery(query) {
            let response = "";
            
            // Sample responses (add more as needed)
            if (query.includes('hello') || query.includes('namaste')) {
                response = "Namaste! Kaise madad karu?";
            } 
            else if (query.includes('time')) {
                response = `Time hai: ${new Date().toLocaleTimeString()}`;
            }
            else if (query.includes('date')) {
                response = `Aaj ki date: ${new Date().toLocaleDateString('hi-IN')}`;
            }
            else if (query.includes('youtube')) {
                response = "YouTube khol raha hoon...";
                setTimeout(() => window.open('https://youtube.com', '_blank'), 1000);
            }
            else {
                response = `<i>Maine samjha: "${query}"</i><br>Par ye feature abhi ban raha hai!`;
            }
            
            setTimeout(() => {
                addMessage(response, false);
                speak(response.replace(/<[^>]*>/g, ''));
                micBtn.classList.remove('bg-green-500');
                micBtn.classList.add('bg-red-500');
            }, 800);
        }

        function addMessage(text, isUser) {
            const msgDiv = document.createElement('div');
            msgDiv.className = `mb-2 p-3 rounded-lg ${isUser ? 'bg-blue-600 ml-auto max-w-xs' : 'bg-gray-700 max-w-xs'}`;
            msgDiv.innerHTML = text;
            chatDiv.appendChild(msgDiv);
            chatDiv.scrollTop = chatDiv.scrollHeight;
        }

        function speak(text) {
            if ('speechSynthesis' in window) {
                const utterance = new SpeechSynthesisUtterance(text);
                utterance.lang = 'hi-IN'; // Hindi accent
                window.speechSynthesis.speak(utterance);
            }
        }
    </script>
</body>
</html>

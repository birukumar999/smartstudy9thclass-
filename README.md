# smartstudy9thclass-
This is my Class 9 AI Study Assistant website using ChatGPT. It helps with Science, Maths, SST, and English.
<!DOCTYPE html>
<html>
<head>
  <title>SmartStudy9 – Tera Class 9 AI Bhai</title>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body { font-family: Arial, sans-serif; background: #f0f0f0; margin: 0; padding: 0; }
    .chatbox { max-width: 600px; margin: auto; padding: 20px; background: white; border-radius: 10px; margin-top: 40px; }
    .chatlog { height: 400px; overflow-y: scroll; border: 1px solid #ddd; padding: 10px; margin-bottom: 10px; background: #fafafa; border-radius: 5px; }
    .user-msg { color: blue; margin: 5px 0; }
    .ai-msg { color: green; margin: 5px 0; }
    input, button { padding: 10px; font-size: 16px; border-radius: 5px; border: 1px solid #ccc; }
    button { background: #4CAF50; color: white; border: none; cursor: pointer; }
    button:hover { background: #45a049; }
  </style>
</head>
<body>
  <div class="chatbox">
    <h2>🤖 SmartStudy9 – Tera AI Bhai for Class 9</h2>
    <div class="chatlog" id="chatlog"></div>
    <input type="text" id="userInput" placeholder="Bhai, koi bhi Class 9 ka sawaal poochh le..." style="width: 80%;">
    <button onclick="sendMessage()">Bhej de</button>
  </div>

  <script>
    const chatlog = document.getElementById('chatlog');

    async function sendMessage() {
      const input = document.getElementById('userInput');
      const userText = input.value;
      if (!userText.trim()) return;

      // User message
      const userMsg = document.createElement('div');
      userMsg.className = 'user-msg';
      userMsg.innerText = '🧑‍🎓 Tu: ' + userText;
      chatlog.appendChild(userMsg);
      chatlog.scrollTop = chatlog.scrollHeight;
      input.value = '';

      // AI thinking
      const thinking = document.createElement('div');
      thinking.className = 'ai-msg';
      thinking.innerText = '🤖 SmartStudy9 soch raha hai...';
      chatlog.appendChild(thinking);
      chatlog.scrollTop = chatlog.scrollHeight;

      // OpenAI API call
      const response = await fetch('https://api.openai.com/v1/chat/completions', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer YOUR_API_KEY_HERE'  // <-- Yahan apni API key lagani hai
        },
        body: JSON.stringify({
          model: 'gpt-3.5-turbo',
          messages: [
            { role: 'system', content: 'Tu ek friendly AI bhai hai jo Class 9 ke students ko unke subjects (Science, Maths, SST, English) mein help karta hai. Jawaab easy aur casual hinglish mein de, samjhane wale style mein.' },
            { role: 'user', content: userText }
          ]
        })
      });

      const data = await response.json();
      thinking.remove();
      const aiText = data.choices[0].message.content;

      const aiMsg = document.createElement('div');
      aiMsg.className = 'ai-msg';
      aiMsg.innerText = '🤖 SmartStudy9: ' + aiText;
      chatlog.appendChild(aiMsg);
      chatlog.scrollTop = chatlog.scrollHeight;
    }
  </script>
</body>
</html>

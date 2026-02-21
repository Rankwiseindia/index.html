<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI अनलिमिटेड MCQ क्विज - फ्री (GS, Reasoning, हिंदी, मैथ)</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(to bottom, #e0f7fa, #ffffff);
      margin: 0;
      padding: 20px;
      color: #333;
      line-height: 1.6;
    }
    .container {
      max-width: 800px;
      margin: 0 auto;
      background: white;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
      color: #0277bd;
      margin-bottom: 10px;
    }
    .subtitle {
      text-align: center;
      color: #555;
      margin-bottom: 30px;
    }
    label {
      display: block;
      margin: 15px 0 5px;
      font-weight: bold;
      color: #444;
    }
    select, input[type="text"] {
      width: 100%;
      padding: 12px;
      border: 1px solid #ccc;
      border-radius: 6px;
      font-size: 16px;
      box-sizing: border-box;
    }
    button {
      display: block;
      width: 100%;
      padding: 14px;
      background: #4CAF50;
      color: white;
      border: none;
      border-radius: 6px;
      font-size: 18px;
      cursor: pointer;
      margin: 25px 0 15px;
      transition: background 0.3s;
    }
    button:hover {
      background: #43A047;
    }
    button:disabled {
      background: #aaa;
      cursor: not-allowed;
    }
    #loading {
      text-align: center;
      font-size: 18px;
      color: #0277bd;
      margin: 20px 0;
      display: none;
    }
    #questions {
      margin-top: 30px;
    }
    .question {
      background: #f9f9f9;
      padding: 18px;
      margin-bottom: 20px;
      border-radius: 8px;
      border-left: 5px solid #4CAF50;
    }
    .question h3 {
      margin-top: 0;
      color: #d32f2f;
    }
    .options {
      margin: 10px 0;
    }
    .correct {
      font-weight: bold;
      color: #2e7d32;
      margin-top: 10px;
    }
    .explanation {
      background: #e8f5e9;
      padding: 10px;
      border-radius: 6px;
      margin-top: 10px;
    }
    @media (max-width: 600px) {
      .container { padding: 15px; }
      button { font-size: 16px; }
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>AI से अनलिमिटेड MCQ क्विज</h1>
    <p class="subtitle">GS • रीजनिंग • हिंदी • गणित — सब हिंदी में, फ्री में!</p>

    <label for="subject">विषय चुनें:</label>
    <select id="subject">
      <option value="सामान्य अध्ययन (GS)">सामान्य अध्ययन (GS)</option>
      <option value="तर्कशक्ति / रीजनिंग">तर्कशक्ति / रीजनिंग</option>
      <option value="हिंदी व्याकरण / साहित्य">हिंदी व्याकरण / साहित्य</option>
      <option value="गणित / मैथ्स">गणित / मैथ्स</option>
    </select>

    <label for="topic">टॉपिक (ऑप्शनल):</label>
    <input type="text" id="topic" placeholder="जैसे: भारतीय संविधान, प्रतिशत, संधि, कोडिंग-डिकोडिंग">

    <label for="level">कठिनाई स्तर:</label>
    <select id="level">
      <option value="आसान">आसान</option>
      <option value="मध्यम" selected>मध्यम</option>
      <option value="कठिन">कठिन</option>
    </select>

    <button id="generateBtn" onclick="generateQuiz()">10 प्रश्न जनरेट करें</button>

    <div id="loading">प्रश्न बन रहे हैं... कृपया 5-15 सेकंड इंतजार करें</div>

    <div id="questions"></div>
  </div>

  <script>
    async function generateQuiz() {
      const btn = document.getElementById('generateBtn');
      const loading = document.getElementById('loading');
      const questionsDiv = document.getElementById('questions');

      btn.disabled = true;
      loading.style.display = 'block';
      questionsDiv.innerHTML = '';

      const subject = document.getElementById('subject').value;
      const topic = document.getElementById('topic').value.trim() || 'सामान्य';
      const level = document.getElementById('level').value;

      const apiKey = 'AIzaSyA8cvIS2eucpZGVe4-WlAcO-7GaeXGmH9k';

      const prompt = `
      तुम एक प्रोफेशनल हिंदी एग्जाम क्वेश्चन मेकर हो।
      विषय: ${subject}
      टॉपिक: ${topic}
      स्तर: ${level}
      
      ठीक 10 MCQ प्रश्न बनाओ, केवल हिंदी में।
      हर प्रश्न के लिए:
      - प्रश्न संख्या और प्रश्न
      - A) विकल्प1
      - B) विकल्प2
      - C) विकल्प3
      - D) विकल्प4
      - सही उत्तर: (A या B या C या D)
      - स्पष्टीकरण: 2-4 लाइन में आसान हिंदी में
      
      सिर्फ प्रश्नों की लिस्ट दो, कोई अतिरिक्त टेक्स्ट मत लिखना।
      `;

      try {
        const response = await fetch(
          `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`,
          {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
              contents: [{ parts: [{ text: prompt }] }]
            })
          }
        );

        if (!response.ok) {
          throw new Error('API से समस्या: ' + response.status);
        }

        const data = await response.json();
        const text = data.candidates?.[0]?.content?.parts?.[0]?.text || 'कोई जवाब नहीं मिला';

        // टेक्स्ट को HTML में बदलकर दिखाओ
        const formatted = text
          .replace(/\n/g, '<br>')
          .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
          .replace(/सही उत्तर:/g, '<div class="correct">सही उत्तर:</div>')
          .replace(/स्पष्टीकरण:/g, '<div class="explanation">स्पष्टीकरण:</div>');

        const questionBlocks = formatted.split(/प्रश्न \d+/).filter(Boolean);
        let html = '';

        questionBlocks.forEach((block, i) => {
          if (block.trim()) {
            html += `<div class="question">
              <h3>प्रश्न ${i + 1}</h3>
              ${block.trim()}
            </div>`;
          }
        });

        questionsDiv.innerHTML = html || '<p style="color:red;">प्रश्न लोड करने में समस्या आई। बाद में ट्राई करें।</p>';

      } catch (error) {
        questionsDiv.innerHTML = `<p style="color:red;">एरर: ${error.message}<br>API की चेक करें या कल ट्राई करें (फ्री लिमिट हो सकती है)।</p>`;
        console.error(error);
      }

      btn.disabled = false;
      loading.style.display = 'none';
    }
  </script>

</body>
</html>

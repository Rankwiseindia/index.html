<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI अनलिमिटेड MCQ क्विज - फ्री (GS, Reasoning, हिंदी, मैथ)</title>
  <style>
    body { font-family: 'Segoe UI', sans-serif; background: linear-gradient(#e0f7fa, #fff); margin:0; padding:20px; color:#333; }
    .container { max-width:800px; margin:auto; background:white; padding:25px; border-radius:12px; box-shadow:0 4px 20px rgba(0,0,0,0.1); }
    h1 { text-align:center; color:#0277bd; }
    .subtitle { text-align:center; color:#555; margin-bottom:30px; }
    label { display:block; margin:15px 0 5px; font-weight:bold; }
    select, input { width:100%; padding:12px; border:1px solid #ccc; border-radius:6px; font-size:16px; box-sizing:border-box; }
    button { width:100%; padding:14px; background:#4CAF50; color:white; border:none; border-radius:6px; font-size:18px; cursor:pointer; margin:25px 0 15px; }
    button:hover { background:#43A047; }
    button:disabled { background:#aaa; }
    #loading { text-align:center; color:#0277bd; font-size:18px; margin:20px 0; display:none; }
    #questions { margin-top:30px; }
    .question { background:#f9f9f9; padding:18px; margin-bottom:20px; border-radius:8px; border-left:5px solid #4CAF50; }
    .correct { font-weight:bold; color:#2e7d32; margin:10px 0; }
    .explanation { background:#e8f5e9; padding:10px; border-radius:6px; }
    .error { color:red; font-weight:bold; }
  </style>
</head>
<body>
  <div class="container">
    <h1>AI से अनलिमिटेड MCQ क्विज</h1>
    <p class="subtitle">GS • रीजनिंग • हिंदी • गणित — सब हिंदी में, फ्री में!</p>

    <label>विषय चुनें:</label>
    <select id="subject">
      <option value="सामान्य अध्ययन (GS)">सामान्य अध्ययन (GS)</option>
      <option value="तर्कशक्ति / रीजनिंग">तर्कशक्ति / रीजनिंग</option>
      <option value="हिंदी व्याकरण / साहित्य">हिंदी व्याकरण / साहित्य</option>
      <option value="गणित / मैथ्स">गणित / मैथ्स</option>
    </select>

    <label>टॉपिक (ऑप्शनल):</label>
    <input type="text" id="topic" placeholder="जैसे: भारतीय संविधान, प्रतिशत, संधि">

    <label>कठिनाई स्तर:</label>
    <select id="level">
      <option value="आसान">आसान</option>
      <option value="मध्यम" selected>मध्यम</option>
      <option value="कठिन">कठिन</option>
    </select>

    <button id="btn" onclick="generateQuiz()">10 प्रश्न जनरेट करें</button>

    <div id="loading">प्रश्न बन रहे हैं... 5-20 सेकंड लग सकते हैं</div>
    <div id="questions"></div>
  </div>

  <script>
    async function generateQuiz() {
      const btn = document.getElementById('btn');
      const loading = document.getElementById('loading');
      const qDiv = document.getElementById('questions');

      btn.disabled = true;
      loading.style.display = 'block';
      qDiv.innerHTML = '';

      const subject = document.getElementById('subject').value;
      const topic = document.getElementById('topic').value.trim() || 'सामान्य';
      const level = document.getElementById('level').value;

      const apiKey = 'AIzaSyA8cvIS2eucpZGVe4-WlAcO-7GaeXGmH9k'; // तुम्हारा की

      const prompt = `तुम हिंदी एग्जाम एक्सपर्ट हो। विषय: ${subject} टॉपिक: ${topic} स्तर: ${level}। ठीक 10 MCQ हिंदी में बनाओ। फॉर्मेट: प्रश्न संख्या। प्रश्न? A) ... B) ... C) ... D) ... सही उत्तर: X स्पष्टीकरण: ... कोई एक्स्ट्रा टेक्स्ट मत लिखना।`;

      try {
        const res = await fetch(
          `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${apiKey}`,
          {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({ contents: [{ parts: [{ text: prompt }] }] })
          }
        );

        if (!res.ok) {
          const err = await res.text();
          throw new Error(`API एरर ${res.status}: ${err}`);
        }

        const data = await res.json();
        let text = data.candidates?.[0]?.content?.parts?.[0]?.text || 'कोई जवाब नहीं';

        // बेहतर फॉर्मेटिंग
        text = text.replace(/\n/g, '<br>').replace(/सही उत्तर:/g, '<div class="correct">सही उत्तर:</div>').replace(/स्पष्टीकरण:/g, '<div class="explanation">स्पष्टीकरण:</div>');

        qDiv.innerHTML = `<h2>जनरेटेड प्रश्न:</h2><div class="question">${text}</div>`;

      } catch (e) {
        qDiv.innerHTML = `<p class="error">एरर: ${e.message}<br>संभावित फिक्स: API की दोबारा जनरेट करो (aistudio.google.com) या मॉडल नाम बदलकर gemini-flash-latest ट्राई करो। लिमिट खत्म हुई हो तो कल ट्राई करो।</p>`;
      }

      btn.disabled = false;
      loading.style.display = 'none';
    }
  </script>
</body>
</html>

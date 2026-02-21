<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>RankWise India - AI Quiz Generator</title>
  <!-- Bootstrap CDN -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, sans-serif;
      background: linear-gradient(to bottom, #f0f8ff, #ffffff);
      color: #333;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }
    .header {
      background: #007bff;
      color: white;
      padding: 25px;
      text-align: center;
      border-bottom: 5px solid #0056b3;
    }
    .container {
      max-width: 950px;
      margin: 25px auto;
      padding: 25px;
      background: white;
      border-radius: 15px;
      box-shadow: 0 6px 30px rgba(0,0,0,0.12);
    }
    .form-control, .btn {
      border-radius: 10px;
    }
    .btn-primary {
      background: #28a745;
      border: none;
    }
    .btn-primary:hover {
      background: #218838;
    }
    .quiz-card {
      margin-bottom: 25px;
      border-left: 6px solid #28a745;
      border-radius: 10px;
    }
    .option-label {
      cursor: pointer;
      padding: 8px 0;
    }
    .correct-answer {
      color: #28a745 !important;
      font-weight: bold;
    }
    .wrong-answer {
      color: #dc3545 !important;
    }
    .explanation {
      background: #e9f7ef;
      padding: 12px;
      border-radius: 8px;
      margin-top: 12px;
      font-size: 0.95em;
    }
    #score {
      text-align: center;
      font-size: 1.6em;
      margin-top: 25px;
    }
    #loading {
      text-align: center;
      color: #007bff;
      font-size: 1.3em;
      display: none;
      margin: 20px 0;
    }
    footer {
      margin-top: auto;
      background: #f8f9fa;
      padding: 25px;
      text-align: center;
      border-top: 1px solid #dee2e6;
      font-size: 0.95em;
      color: #495057;
    }
    .progress {
      height: 25px;
      margin-top: 15px;
    }
    .exam-list {
      font-size: 0.9em;
      margin-top: 10px;
      color: #6c757d;
    }
  </style>
</head>
<body>

  <header class="header">
    <h1>RankWise India - AI से अनलिमिटेड MCQ क्विज</h1>
    <p>GS, रीजनिंग, हिंदी, गणित के लिए हिंदी में अनलिमिटेड ऑब्जेक्टिव प्रश्न — पूरी तरह फ्री!</p>
  </header>

  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-10">
        <label for="subject" class="form-label fw-bold">विषय चुनें:</label>
        <select id="subject" class="form-select mb-3">
          <option value="सामान्य अध्ययन (GS)">सामान्य अध्ययन (GS)</option>
          <option value="तर्कशक्ति / रीजनिंग">तर्कशक्ति / रीजनिंग</option>
          <option value="हिंदी व्याकरण / साहित्य">हिंदी व्याकरण / साहित्य</option>
          <option value="गणित / मैथ्स">गणित / मैथ्स</option>
        </select>

        <label for="topic" class="form-label fw-bold">टॉपिक (ऑप्शनल):</label>
        <input type="text" id="topic" class="form-control mb-3" placeholder="जैसे: भारतीय संविधान, प्रतिशत, संधि, कोडिंग-डिकोडिंग">

        <label for="level" class="form-label fw-bold">कठिनाई स्तर:</label>
        <select id="level" class="form-select mb-3">
          <option value="आसान">आसान</option>
          <option value="मध्यम" selected>मध्यम</option>
          <option value="कठिन">कठिन</option>
        </select>

        <button id="generateBtn" class="btn btn-primary btn-lg w-100 mb-4" onclick="generateQuiz()">10 प्रश्न जनरेट करें</button>

        <div id="loading" class="alert alert-info">प्रश्न जनरेट हो रहे हैं... 5-25 सेकंड लग सकते हैं</div>

        <form id="quizForm">
          <div id="questions"></div>
          <button type="button" id="submitBtn" class="btn btn-success btn-lg w-100 mt-4" onclick="submitQuiz()" style="display: none;">क्विज सबमिट करें & स्कोर देखें</button>
        </form>

        <div id="score" class="alert alert-success" style="display: none;"></div>
      </div>
    </div>
  </div>

  <footer>
    <p>Created by Naveen from Nagla Ugrasen, Post Kuchesar, District Bulandshahr, Uttar Pradesh. This is an AI-powered platform for unlimited objective quizzes in Hindi for GS, Reasoning, Hindi, and Math.</p>
    <p class="exam-list">हम SSC CGL, SSC CHSL, SSC MTS, SSC GD Constable, SSC CPO, Delhi Police Constable, Delhi Police Head Constable, RRB NTPC, RRB Group D, RRB ALP, RRB JE, IBPS PO/Clerk, SBI PO/Clerk, RPF Constable/SI, UPSC CDS/NDA और अन्य प्रमुख सरकारी भर्तियों के लिए प्रैक्टिस क्विज प्रदान करते हैं।</p>
    <p>For queries, contact: [अपना ईमेल डालें या हटाएं]। &copy; 2026 RankWise India.</p>
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
  <script>
    let questionsData = [];

    async function generateQuiz() {
      const btn = document.getElementById('generateBtn');
      const loading = document.getElementById('loading');
      const questionsDiv = document.getElementById('questions');
      const submitBtn = document.getElementById('submitBtn');
      const scoreDiv = document.getElementById('score');

      btn.disabled = true;
      loading.style.display = 'block';
      questionsDiv.innerHTML = '';
      submitBtn.style.display = 'none';
      scoreDiv.style.display = 'none';

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
      आउटपुट सिर्फ JSON ऐरे में दो, कुछ और मत लिखना:
      [
        {
          "question": "प्रश्न टेक्स्ट",
          "options": ["A) ऑप्शन1", "B) ऑप्शन2", "C) ऑप्शन3", "D) ऑप्शन4"],
          "correct": "A",
          "explanation": "स्पष्टीकरण 2-4 लाइन में"
        }
      ]
      `;

      try {
        const response = await fetch(
          `https://generativelanguage.googleapis.com/v1beta/models/gemini-flash-latest:generateContent?key=${apiKey}`,
          {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
              contents: [{ parts: [{ text: prompt }] }]
            })
          }
        );

        if (!response.ok) {
          throw new Error('API एरर: ' + response.status + ' - मॉडल नाम या की चेक करें');
        }

        const data = await response.json();
        const text = data.candidates[0].content.parts[0].text;
        const jsonMatch = text.match(/\[[\s\S]*\]/);
        questionsData = jsonMatch ? JSON.parse(jsonMatch[0]) : [];

        if (questionsData.length === 0) throw new Error('प्रश्न नहीं मिले');

        questionsData.forEach((q, i) => {
          const card = document.createElement('div');
          card.className = 'card quiz-card mb-4';
          card.innerHTML = `
            <div class="card-body">
              <h5 class="card-title">प्रश्न ${i + 1}: ${q.question}</h5>
              ${q.options.map((opt, j) => `
                <div class="form-check">
                  <input class="form-check-input" type="radio" name="q\( {i}" id="q \){i}_\( {j}" value=" \){opt.charAt(0)}">
                  <label class="form-check-label option-label" for="q\( {i}_ \){j}">${opt}</label>
                </div>
              `).join('')}
              <div class="explanation" id="exp\( {i}" style="display:none;"> \){q.explanation}</div>
            </div>
          `;
          questionsDiv.appendChild(card);
        });

        submitBtn.style.display = 'block';

      } catch (error) {
        questionsDiv.innerHTML = `<div class="alert alert-danger">एरर: ${error.message}. API की या मॉडल (gemini-flash-latest) चेक करें।</div>`;
      }

      btn.disabled = false;
      loading.style.display = 'none';
    }

    function submitQuiz() {
      const scoreDiv = document.getElementById('score');
      let score = 0;
      let total = questionsData.length;

      questionsData.forEach((q, i) => {
        const selected = document.querySelector(`input[name="q${i}"]:checked`);
        const exp = document.getElementById(`exp${i}`);
        exp.style.display = 'block';

        if (selected && selected.value === q.correct) {
          score++;
          selected.nextElementSibling.classList.add('correct-answer');
        } else if (selected) {
          selected.nextElementSibling.classList.add('wrong-answer');
        }

        const correctOpt = document.querySelector(`input[value="\( {q.correct}"][name="q \){i}"]`);
        if (correctOpt) correctOpt.nextElementSibling.classList.add('correct-answer');
      });

      const percentage = ((score / total) * 100).toFixed(2);
      scoreDiv.innerHTML = `आपका स्कोर: <strong>\( {score}/ \){total}</strong> (${percentage}%)`;
      scoreDiv.className = percentage >= 70 ? 'alert alert-success' : 'alert alert-warning';
      scoreDiv.style.display = 'block';

      const progress = document.createElement('div');
      progress.className = 'progress';
      progress.innerHTML = `<div class="progress-bar ${percentage >= 70 ? 'bg-success' : 'bg-warning'}" role="progressbar" style="width: \( {percentage}%" aria-valuenow=" \){percentage}" aria-valuemin="0" aria-valuemax="100">${percentage}%</div>`;
      scoreDiv.appendChild(progress);
    }
  </script>
</body>
</html>

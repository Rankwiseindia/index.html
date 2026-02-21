<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>RankWise India - AI अनलिमिटेड MCQ क्विज</title>

  <!-- Bootstrap 5 CDN -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">

  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #e0f7fa 0%, #ffffff 100%);
      color: #2c3e50;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      margin: 0;
    }

    header.header {
      background: linear-gradient(to right, #007bff, #0056b3);
      color: white;
      padding: 40px 20px;
      text-align: center;
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2);
    }

    header h1 {
      font-size: 2.6rem;
      margin-bottom: 10px;
      font-weight: 700;
    }

    header p {
      font-size: 1.2rem;
      opacity: 0.95;
    }

    .container-main {
      max-width: 1100px;
      margin: 40px auto;
      padding: 0 20px;
      flex: 1;
    }

    .card-form {
      background: white;
      border-radius: 16px;
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.12);
      padding: 35px;
      margin-bottom: 30px;
    }

    .form-label {
      font-weight: 600;
      color: #34495e;
      margin-bottom: 10px;
      display: block;
    }

    .form-select, .form-control {
      border-radius: 12px;
      padding: 14px 16px;
      font-size: 1.05rem;
      border: 1px solid #ced4da;
      transition: border-color 0.3s, box-shadow 0.3s;
    }

    .form-select:focus, .form-control:focus {
      border-color: #28a745;
      box-shadow: 0 0 0 0.25rem rgba(40, 167, 69, 0.25);
    }

    .btn-generate {
      background: #28a745;
      border: none;
      font-size: 1.3rem;
      padding: 16px;
      border-radius: 12px;
      transition: all 0.3s;
      font-weight: 600;
    }

    .btn-generate:hover {
      background: #218838;
      transform: translateY(-3px);
      box-shadow: 0 8px 20px rgba(33, 136, 56, 0.3);
    }

    .loading-message {
      font-size: 1.4rem;
      color: #007bff;
      text-align: center;
      margin: 30px 0;
      display: none;
    }

    .quiz-question-card {
      background: white;
      border-radius: 14px;
      box-shadow: 0 6px 25px rgba(0, 0, 0, 0.1);
      margin-bottom: 30px;
      border-left: 8px solid #28a745;
      overflow: hidden;
    }

    .quiz-question-card .card-body {
      padding: 28px;
    }

    .question-title {
      font-size: 1.35rem;
      font-weight: 600;
      margin-bottom: 20px;
      color: #2c3e50;
    }

    .option-item {
      margin: 12px 0;
      padding: 14px 18px;
      border-radius: 10px;
      cursor: pointer;
      transition: all 0.25s;
      background: #f8f9fa;
      border: 1px solid #dee2e6;
    }

    .option-item:hover {
      background: #e9ecef;
      transform: translateX(5px);
    }

    .correct-answer {
      background: #d4edda !important;
      border-color: #28a745 !important;
      color: #155724 !important;
      font-weight: bold;
    }

    .wrong-answer {
      background: #f8d7da !important;
      border-color: #dc3545 !important;
      color: #721c24 !important;
    }

    .explanation-box {
      background: #e9f7ef;
      padding: 18px;
      border-radius: 10px;
      margin-top: 20px;
      font-size: 1rem;
      line-height: 1.7;
      border-left: 5px solid #28a745;
    }

    #score-result {
      text-align: center;
      font-size: 2.2rem;
      padding: 30px;
      border-radius: 16px;
      margin: 40px 0;
      box-shadow: 0 8px 30px rgba(0,0,0,0.1);
    }

    footer {
      background: #2c3e50;
      color: white;
      text-align: center;
      padding: 35px 20px;
      margin-top: auto;
      font-size: 0.98rem;
    }

    footer a {
      color: #18bc9c;
      text-decoration: none;
    }

    footer a:hover {
      text-decoration: underline;
    }

    .exam-list {
      font-size: 0.94rem;
      line-height: 1.8;
      color: #bdc3c7;
    }

    @media (max-width: 768px) {
      .card-form { padding: 25px; }
      header h1 { font-size: 2.2rem; }
      .quiz-question-card .card-body { padding: 20px; }
    }
  </style>
</head>
<body>

  <header class="header">
    <h1>RankWise India</h1>
    <p>AI से अनलिमिटेड हिंदी MCQ क्विज — SSC, RRB, Delhi Police, Banking, Defence और सभी सरकारी परीक्षाओं के लिए</p>
  </header>

  <div class="container-main">
    <div class="card-form">
      <div class="mb-4">
        <label for="subject" class="form-label">विषय चुनें</label>
        <select id="subject" class="form-select">
          <option value="सामान्य अध्ययन (GS)">सामान्य अध्ययन (GS)</option>
          <option value="तर्कशक्ति / रीजनिंग">तर्कशक्ति / रीजनिंग</option>
          <option value="हिंदी व्याकरण / साहित्य">हिंदी व्याकरण / साहित्य</option>
          <option value="गणित / मैथ्स">गणित / मैथ्स</option>
        </select>
      </div>

      <div class="mb-4">
        <label for="topic" class="form-label">टॉपिक (ऑप्शनल)</label>
        <input type="text" id="topic" class="form-control" placeholder="जैसे: भारतीय संविधान, प्रतिशत, संधि, कोडिंग-डिकोडिंग, भारतीय इतिहास, भूगोल">
      </div>

      <div class="mb-4">
        <label for="level" class="form-label">कठिनाई स्तर</label>
        <select id="level" class="form-select">
          <option value="आसान">आसान</option>
          <option value="मध्यम" selected>मध्यम</option>
          <option value="कठिन">कठिन</option>
        </select>
      </div>

      <button id="generateBtn" class="btn btn-generate w-100">10 प्रश्न जनरेट करें</button>

      <div id="loading" class="loading-message">प्रश्न तैयार हो रहे हैं... कृपया 5 से 35 सेकंड इंतजार करें</div>

      <form id="quizForm" class="mt-5">
        <div id="questions"></div>
        <button type="button" id="submitBtn" class="btn btn-success w-100 mt-4 py-3 fw-bold" style="display:none; font-size:1.3rem;">
          क्विज सबमिट करें और स्कोर देखें
        </button>
      </form>

      <div id="score" class="mt-5" style="display:none;"></div>
    </div>
  </div>

  <footer>
    <p>Created with ❤️ by Naveen from Nagla Ugrasen, Post Kuchesar, District Bulandshahr, Uttar Pradesh</p>
    <p class="exam-list mt-3">
      यह AI आधारित प्लेटफॉर्म हिंदी में अनलिमिटेड ऑब्जेक्टिव क्विज प्रदान करता है GS, रीजनिंग, हिंदी व्याकरण/साहित्य और गणित के लिए।<br>
      विशेष रूप से उपयोगी: SSC CGL, SSC CHSL, SSC MTS, SSC GD Constable, SSC CPO, Delhi Police Constable, Delhi Police Head Constable,<br>
      RRB NTPC, RRB Group D, RRB ALP, RRB JE, IBPS PO/Clerk, SBI PO/Clerk, RPF Constable/SI, UPSC CDS/NDA और अन्य सभी सरकारी भर्ती परीक्षाओं के लिए।
    </p>
    <p class="mt-3">सवाल-जवाब के लिए संपर्क: [अपना ईमेल डालें या हटाएं] • © 2026 RankWise India</p>
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>

  <script>
    // ================================================
    // मुख्य वेरिएबल्स
    // ================================================
    let questionsData = [];

    // ================================================
    // प्रश्न जनरेट करने का मुख्य फंक्शन
    // ================================================
    async function generateQuiz() {
      const generateBtn = document.getElementById('generateBtn');
      const loadingDiv = document.getElementById('loading');
      const questionsContainer = document.getElementById('questions');
      const submitButton = document.getElementById('submitBtn');
      const scoreContainer = document.getElementById('score');

      // बटन डिसेबल + लोडिंग दिखाओ
      generateBtn.disabled = true;
      loadingDiv.style.display = 'block';
      questionsContainer.innerHTML = '';
      submitButton.style.display = 'none';
      scoreContainer.style.display = 'none';

      // API Key मांगो (प्राइवेट रखने के लिए)
      const apiKey = prompt("Gemini API Key डालें (https://aistudio.google.com/app/apikey से कॉपी करके पेस्ट करें)")?.trim();

      if (!apiKey) {
        questionsContainer.innerHTML = '<div class="alert alert-warning text-center fs-5 p-4">API Key नहीं डाली गई। पेज रिफ्रेश करके दोबारा ट्राई करें।</div>';
        generateBtn.disabled = false;
        loadingDiv.style.display = 'none';
        return;
      }

      const subject = document.getElementById('subject').value;
      const topicInput = document.getElementById('topic').value.trim();
      const topic = topicInput || 'सामान्य';
      const level = document.getElementById('level').value;

      // प्रॉम्प्ट तैयार करो
      const promptText = `
तुम एक प्रोफेशनल हिंदी प्रतियोगी परीक्षा विशेषज्ञ हो।
विषय: ${subject}
टॉपिक: ${topic}
स्तर: ${level}

ठीक 10 MCQ प्रश्न बनाओ, पूरी तरह हिंदी में।
प्रत्येक प्रश्न में 4 विकल्प (A, B, C, D) हों।
आउटपुट केवल JSON ऐरे के रूप में दो, कुछ भी एक्स्ट्रा मत लिखना:

[
  {
    "question": "प्रश्न यहाँ",
    "options": ["A) विकल्प 1", "B) विकल्प 2", "C) विकल्प 3", "D) विकल्प 4"],
    "correct": "A",
    "explanation": "स्पष्टीकरण 2-5 लाइन में"
  }
]
      `;

      try {
        const response = await fetch(
          `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${apiKey}`,
          // वैकल्पिक मॉडल (अगर ऊपर वाला न चले तो इनमें से एक ट्राई करो):
          // `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-lite:generateContent?key=${apiKey}`
          // `https://generativelanguage.googleapis.com/v1beta/models/gemini-flash-latest:generateContent?key=${apiKey}`
          {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
              contents: [{ parts: [{ text: promptText }] }]
            })
          }
        );

        if (!response.ok) {
          const errorBody = await response.text();
          throw new Error(`API त्रुटि ${response.status}: ${errorBody}`);
        }

        const jsonData = await response.json();
        let rawText = jsonData.candidates?.[0]?.content?.parts?.[0]?.text || '';

        // JSON हिस्सा निकालो
        const jsonArrayMatch = rawText.match(/\[[\s\S]*\]/);
        questionsData = jsonArrayMatch ? JSON.parse(jsonArrayMatch[0]) : [];

        if (!Array.isArray(questionsData) || questionsData.length === 0) {
          throw new Error('कोई वैध प्रश्न नहीं मिला');
        }

        // प्रश्न दिखाओ
        questionsData.forEach((q, index) => {
          const questionCard = document.createElement('div');
          questionCard.className = 'quiz-question-card';

          let optionsHTML = q.options.map((opt, j) => {
            const letter = opt.charAt(0);
            return `
              <div class="option-item" data-letter="${letter}">
                <input type="radio" name="q\( {index}" id="opt \){index}_\( {j}" value=" \){letter}" class="d-none">
                <label for="opt\( {index}_ \){j}" class="option-label m-0">${opt}</label>
              </div>
            `;
          }).join('');

          questionCard.innerHTML = `
            <div class="card-body">
              <div class="question-title">प्रश्न ${index + 1}: ${q.question}</div>
              ${optionsHTML}
              <div class="explanation-box" id="exp${index}" style="display:none;">
                ${q.explanation || 'स्पष्टीकरण उपलब्ध नहीं'}
              </div>
            </div>
          `;

          questionsContainer.appendChild(questionCard);

          // हर विकल्प पर क्लिक करने पर हाइलाइट
          questionCard.querySelectorAll('.option-item').forEach(item => {
            item.addEventListener('click', () => {
              const radio = item.querySelector('input[type="radio"]');
              radio.checked = true;

              // सभी विकल्पों से हाइलाइट हटाओ
              questionCard.querySelectorAll('.option-item').forEach(el => {
                el.classList.remove('correct-answer', 'wrong-answer');
              });

              const selectedLetter = radio.value;
              if (selectedLetter === q.correct) {
                item.classList.add('correct-answer');
              } else {
                item.classList.add('wrong-answer');
                // सही विकल्प भी हाइलाइट करो
                const correctItem = questionCard.querySelector(`.option-item[data-letter="${q.correct}"]`);
                if (correctItem) correctItem.classList.add('correct-answer');
              }
            });
          });
        });

        submitButton.style.display = 'block';

      } catch (err) {
        questionsContainer.innerHTML = `
          <div class="alert alert-danger p-4 text-center fs-5">
            <strong>त्रुटि हुई:</strong> ${err.message}<br><br>
            संभावित कारण और समाधान:<br>
            1. API key गलत है या लीक्ड हो गई है → नया key बनाएं (aistudio.google.com)<br>
            2. मॉडल नाम बदलकर ट्राई करें (ऊपर कमेंट में देखें)<br>
            3. इंटरनेट कनेक्शन चेक करें<br>
            4. पेज रिफ्रेश करके दोबारा key डालकर ट्राई करें
          </div>
        `;
      }

      generateBtn.disabled = false;
      loadingDiv.style.display = 'none';
    }

    // ================================================
    // सबमिट फंक्शन - स्कोर कैलकुलेट करो
    // ================================================
    function submitQuiz() {
      const scoreDiv = document.getElementById('score');
      let correctCount = 0;

      questionsData.forEach((q, i) => {
        const selectedRadio = document.querySelector(`input[name="q${i}"]:checked`);
        const explanation = document.getElementById(`exp${i}`);

        if (explanation) explanation.style.display = 'block';

        if (selectedRadio && selectedRadio.value === q.correct) {
          correctCount++;
        }

        // सही विकल्प हमेशा हाइलाइट रहे
        const correctItem = document.querySelector(`.quiz-question-card:nth-child(\( {i+1}) .option-item[data-letter=" \){q.correct}"]`);
        if (correctItem) correctItem.classList.add('correct-answer');
      });

      const percentage = ((correctCount / questionsData.length) * 100).toFixed(1);

      scoreDiv.innerHTML = `
        <div class="bg-white p-5 rounded shadow">
          <h2 class="mb-4">आपका परिणाम</h2>
          <h3 class="display-4 fw-bold ${percentage >= 70 ? 'text-success' : 'text-danger'}">
            ${correctCount} / ${questionsData.length}
          </h3>
          <p class="fs-4 mt-3">प्रतिशत: <strong>${percentage}%</strong></p>
          <div class="progress mt-4" style="height: 30px;">
            <div class="progress-bar ${percentage >= 70 ? 'bg-success' : 'bg-warning'}" role="progressbar" 
                 style="width: \( {percentage}%" aria-valuenow=" \){percentage}" aria-valuemin="0" aria-valuemax="100">
              ${percentage}%
            </div>
          </div>
          <p class="mt-4 fs-5">
            ${percentage >= 80 ? 'शानदार! बहुत अच्छा प्रदर्शन।' : 
              percentage >= 60 ? 'अच्छा प्रयास! थोड़ा और प्रैक्टिस करें।' : 
              'कोशिश जारी रखें! अगली बार बेहतर होगा।'}
          </p>
        </div>
      `;

      scoreDiv.style.display = 'block';
      window.scrollTo({ top: scoreDiv.offsetTop - 100, behavior: 'smooth' });
    }

    // ================================================
    // इवेंट लिसनर
    // ================================================
    document.getElementById('generateBtn').addEventListener('click', generateQuiz);
    document.getElementById('submitBtn').addEventListener('click', submitQuiz);
  </script>
</body>
</html>

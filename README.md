<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>RankWise India - AI Quiz Generator</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
  <style>
    body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: linear-gradient(to bottom, #f0f8ff, #ffffff); color: #333; min-height: 100vh; display: flex; flex-direction: column; }
    .header { background: #007bff; color: white; padding: 30px 15px; text-align: center; border-bottom: 6px solid #0056b3; box-shadow: 0 4px 12px rgba(0,0,0,0.15); }
    .container { max-width: 980px; margin: 30px auto; padding: 30px; background: white; border-radius: 16px; box-shadow: 0 8px 35px rgba(0,0,0,0.12); }
    .form-label { font-weight: 600; margin-bottom: 8px; color: #333; }
    .form-select, .form-control { border-radius: 10px; padding: 12px; font-size: 1rem; }
    .btn-primary { background: #28a745; border: none; font-size: 1.2rem; padding: 14px; border-radius: 10px; transition: all 0.3s; }
    .btn-primary:hover { background: #218838; transform: translateY(-2px); }
    .quiz-card { margin-bottom: 28px; border-left: 7px solid #28a745; border-radius: 12px; overflow: hidden; box-shadow: 0 3px 15px rgba(0,0,0,0.08); }
    .quiz-card .card-body { padding: 22px; }
    .option-label { cursor: pointer; padding: 10px 15px; display: block; margin: 8px 0; border-radius: 8px; transition: all 0.2s; }
    .form-check-input:checked + .option-label { background: #e9ecef; }
    .correct-answer { background: #d4edda !important; color: #155724 !important; font-weight: bold; border: 2px solid #28a745; }
    .wrong-answer { background: #f8d7da !important; color: #721c24 !important; border: 2px solid #dc3545; }
    .explanation { background: #e9f7ef; padding: 15px; border-radius: 10px; margin-top: 15px; font-size: 0.97rem; line-height: 1.6; }
    #score { text-align: center; font-size: 1.8rem; margin-top: 30px; padding: 20px; border-radius: 12px; }
    #loading { text-align: center; color: #007bff; font-size: 1.4rem; margin: 25px 0; display: none; }
    footer { margin-top: auto; background: #f8f9fa; padding: 30px 15px; text-align: center; border-top: 1px solid #dee2e6; font-size: 0.96rem; color: #495057; }
    .progress { height: 28px; margin-top: 18px; border-radius: 14px; }
    .exam-list { font-size: 0.92rem; margin-top: 12px; color: #6c757d; line-height: 1.7; }
    @media (max-width: 576px) { .container { padding: 20px; margin: 15px; } .header { padding: 20px 10px; } h1 { font-size: 1.8rem; } }
  </style>
</head>
<body>

  <header class="header">
    <h1>RankWise India - AI से अनलिमिटेड MCQ क्विज</h1>
    <p>SSC, RRB, Delhi Police, Banking, Defence और सभी सरकारी परीक्षाओं के लिए हिंदी में अनलिमिटेड ऑब्जेक्टिव प्रश्न — पूरी तरह फ्री!</p>
  </header>

  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-10 col-lg-9">
        <label for="subject" class="form-label">विषय चुनें:</label>
        <select id="subject" class="form-select mb-4">
          <option value="सामान्य अध्ययन (GS)">सामान्य अध्ययन (GS)</option>
          <option value="तर्कशक्ति / रीजनिंग">तर्कशक्ति / रीजनिंग</option>
          <option value="हिंदी व्याकरण / साहित्य">हिंदी व्याकरण / साहित्य</option>
          <option value="गणित / मैथ्स">गणित / मैथ्स</option>
        </select>

        <label for="topic" class="form-label">टॉपिक (ऑप्शनल):</label>
        <input type="text" id="topic" class="form-control mb-4" placeholder="जैसे: भारतीय संविधान, प्रतिशत, संधि, कोडिंग-डिकोडिंग, भारतीय इतिहास">

        <label for="numQuestions" class="form-label">प्रश्नों की संख्या चुनें:</label>
        <select id="numQuestions" class="form-select mb-4">
          <option value="10" selected>10 प्रश्न</option>
          <option value="20">20 प्रश्न</option>
          <option value="40">40 प्रश्न</option>
          <option value="50">50 प्रश्न</option>
          <option value="custom">कस्टम संख्या</option>
        </select>

        <div id="customNumDiv" style="display:none;" class="mb-4">
          <label for="customNum" class="form-label">कितने प्रश्न चाहिए? (10 से 100 तक):</label>
          <input type="number" id="customNum" class="form-control" min="10" max="100" value="10">
        </div>

        <label for="level" class="form-label">कठिनाई स्तर:</label>
        <select id="level" class="form-select mb-4">
          <option value="आसान">आसान</option>
          <option value="मध्यम" selected>मध्यम</option>
          <option value="कठिन">कठिन</option>
        </select>

        <button id="generateBtn" class="btn btn-primary btn-lg w-100 mb-4 py-3">प्रश्न जनरेट करें</button>

        <div id="loading" class="alert alert-info text-center fs-5">प्रश्न जनरेट हो रहे हैं... कृपया 5 से 60 सेकंड तक इंतजार करें</div>

        <form id="quizForm">
          <div id="questions"></div>
          <button type="button" id="submitBtn" class="btn btn-success btn-lg w-100 mt-4 py-3" style="display: none;">क्विज सबमिट करें और स्कोर देखें</button>
        </form>

        <div id="score" class="alert" style="display: none;"></div>
      </div>
    </div>
  </div>

  <footer>
    <p>Created by Naveen from Nagla Ugrasen, Post Kuchesar, District Bulandshahr, Uttar Pradesh.</p>
    <p class="exam-list">हम SSC CGL, SSC CHSL, SSC MTS, SSC GD Constable, SSC CPO, Delhi Police Constable, Delhi Police Head Constable, RRB NTPC, RRB Group D, RRB ALP, RRB JE, IBPS PO/Clerk, SBI PO/Clerk, RPF Constable/SI, UPSC CDS/NDA और अन्य प्रमुख सरकारी भर्तियों/परीक्षाओं के लिए प्रैक्टिस क्विज प्रदान करते हैं।</p>
    <p>© 2026 RankWise India.</p>
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
  <script>
    let questionsData = [];

    // प्रश्न संख्या चुनने पर कस्टम दिखाओ
    document.getElementById('numQuestions').addEventListener('change', function() {
      document.getElementById('customNumDiv').style.display = this.value === 'custom' ? 'block' : 'none';
    });

    // बटन पर क्लिक करने के लिए इवेंट लिसनर (onclick हटाकर)
    document.getElementById('generateBtn').addEventListener('click', async function() {
      const btn = this;
      const loading = document.getElementById('loading');
      const questionsDiv = document.getElementById('questions');
      const submitBtn = document.getElementById('submitBtn');
      const scoreDiv = document.getElementById('score');

      btn.disabled = true;
      loading.style.display = 'block';
      questionsDiv.innerHTML = '';
      submitBtn.style.display = 'none';
      scoreDiv.style.display = 'none';

      const apiKey = prompt('Groq API Key डालो (https://console.groq.com/keys से कॉपी करो)')?.trim();
      if (!apiKey) {
        questionsDiv.innerHTML = '<div class="alert alert-danger">API Key नहीं डाली गई।</div>';
        btn.disabled = false;
        loading.style.display = 'none';
        return;
      }

      let numQuestions = document.getElementById('numQuestions').value;
      if (numQuestions === 'custom') {
        numQuestions = parseInt(document.getElementById('customNum').value) || 10;
        if (numQuestions < 10 || numQuestions > 100) numQuestions = 10;
      } else {
        numQuestions = parseInt(numQuestions);
      }

      const subject = document.getElementById('subject').value;
      const topic = document.getElementById('topic').value.trim() || 'सामान्य';
      const level = document.getElementById('level').value;

      const prompt = `तुम एक प्रोफेशनल हिंदी एग्जाम क्वेश्चन मेकर हो।  
विषय: ${subject}  
टॉपिक: ${topic}  
स्तर: ${level}  

ठीक ${numQuestions} MCQ प्रश्न बनाओ, केवल हिंदी में।  
प्रत्येक प्रश्न में 4 विकल्प (A, B, C, D) हों।  
आउटपुट सिर्फ JSON ऐरे में दो:  
[  
  {  
    "question": "प्रश्न टेक्स्ट",  
    "options": ["A) ऑप्शन1", "B) ऑप्शन2", "C) ऑप्शन3", "D) ऑप्शन4"],  
    "correct": "A",  
    "explanation": "स्पष्टीकरण 2-4 लाइन में"  
  }  
]`;

      try {
        const response = await fetch("https://api.groq.com/openai/v1/chat/completions", {
          method: "POST",
          headers: {
            "Authorization": `Bearer ${apiKey}`,
            "Content-Type": "application/json"
          },
          body: JSON.stringify({
            model: "llama-3.1-70b-versatile",
            messages: [{ role: "user", content: prompt }],
            temperature: 0.7,
            max_tokens: 4096
          })
        });

        if (!response.ok) {
          const err = await response.json();
          throw new Error(err.error?.message || 'API एरर');
        }

        const data = await response.json();
        const text = data.choices[0].message.content.trim();

        const jsonMatch = text.match(/\[[\s\S]*\]/);
        if (!jsonMatch) throw new Error('JSON नहीं मिला');

        questionsData = JSON.parse(jsonMatch[0]);

        if (!Array.isArray(questionsData) || questionsData.length === 0) {
          throw new Error('प्रश्न नहीं मिले');
        }

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
        questionsDiv.innerHTML = `<div class="alert alert-danger">
          <strong>एरर:</strong> ${error.message}<br>
          <small>फिक्स: Groq key सही डालो या नया बनाओ। अगर rate limit आए तो 1-2 मिनट इंतजार करो।</small>
        </div>`;
      }

      btn.disabled = false;
      loading.style.display = 'none';
    });

    function submitQuiz() {
      const scoreDiv = document.getElementById('score');
      let score = 0;
      let total = questionsData.length;

      questionsData.forEach((q, i) => {
        const selected = document.querySelector(`input[name="q${i}"]:checked`);
        const exp = document.getElementById(`exp${i}`);
        if (exp) exp.style.display = 'block';

        const correctLabel = document.querySelector(`input[value="\( {q.correct}"][name="q \){i}"]`)?.nextElementSibling;
        if (correctLabel) correctLabel.classList.add('correct-answer');

        if (selected) {
          const selectedLabel = selected.nextElementSibling;
          if (selected.value === q.correct) {
            score++;
          } else {
            selectedLabel.classList.add('wrong-answer');
          }
        }
      });

      const percentage = ((score / total) * 100).toFixed(2);
      scoreDiv.innerHTML = `
        आपका स्कोर: <strong>\( {score}/ \){total}</strong> (${percentage}%)<br>
        ${percentage >= 70 ? 'बहुत अच्छा!' : 'अगली बार और बेहतर करेंगे।'}
      `;
      scoreDiv.className = percentage >= 70 ? 'alert alert-success' : 'alert alert-warning';
      scoreDiv.style.display = 'block';

      const progress = document.createElement('div');
      progress.className = 'progress mt-3';
      progress.innerHTML = `<div class="progress-bar ${percentage >= 70 ? 'bg-success' : 'bg-warning'}" role="progressbar" style="width: \( {percentage}%" aria-valuenow=" \){percentage}" aria-valuemin="0" aria-valuemax="100">${percentage}%</div>`;
      scoreDiv.appendChild(progress);
    }

    document.getElementById('submitBtn').addEventListener('click', submitQuiz);
  </script>
</body>
</html>

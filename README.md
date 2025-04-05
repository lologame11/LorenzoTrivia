# LorenzoTrivia
Lorenzo
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Preguntas Lorenzo</title>
  <link rel="canonical" href="https://tujuego.com/preguntas-lorenzo">
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #74ebd5, #9face6);
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      position: relative;
    }
    .trivia-container {
      background: white;
      padding: 2rem;
      border-radius: 20px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
      max-width: 600px;
      width: 90%;
      text-align: center;
      animation: fadeIn 1s ease-in-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.95); }
      to { opacity: 1; transform: scale(1); }
    }
    h1 {
      color: #333;
      margin-bottom: 1rem;
    }
    .question {
      font-size: 1.4rem;
      margin-bottom: 1rem;
      color: #444;
    }
    .options button {
      background-color: #f7f7f7;
      border: 2px solid #ccc;
      border-radius: 10px;
      padding: 0.75rem 1rem;
      margin: 0.5rem 0;
      font-size: 1rem;
      width: 100%;
      transition: all 0.2s ease;
      cursor: pointer;
    }
    .options button:hover {
      background-color: #d1e8ff;
      border-color: #74aee9;
    }
    .feedback {
      margin-top: 1rem;
      font-weight: bold;
      font-size: 1.1rem;
    }
    .score {
      margin-bottom: 1rem;
      font-size: 1rem;
      font-weight: bold;
      color: #555;
    }
    .progress-bar {
      height: 10px;
      background: #e0e0e0;
      border-radius: 5px;
      overflow: hidden;
      margin: 1rem 0;
    }
    .progress-fill {
      height: 100%;
      background: #74aee9;
      width: 0;
      transition: width 0.3s ease;
    }
    .author-label {
      position: absolute;
      top: 10px;
      right: 10px;
      background-color: rgba(0, 0, 0, 0.6);
      color: #fff;
      padding: 10px 15px;
      border-radius: 10px;
      font-size: 0.9rem;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="author-label">Hecho por Lorenzo - 5/4/25</div>
  <div class="trivia-container">
    <h1>🎉 Preguntas Lorenzo 🎉</h1>
    <div class="score" id="score">Puntaje: 0</div>
    <div class="progress-bar"><div class="progress-fill" id="progress-fill"></div></div>
    <div class="question" id="question">Cargando pregunta...</div>
    <div class="options" id="options"></div>
    <div class="feedback" id="feedback"></div>
  </div>

  <script>
    const questions = [
      { question: "¿En qué año comenzó la Segunda Guerra Mundial?", options: ["1918", "1939", "1945", "1929"], answer: "1939" },
      { question: "¿Quién fue el primer emperador romano?", options: ["Julio César", "Nerón", "Augusto", "Trajano"], answer: "Augusto" },
      { question: "¿Qué película ganó el Oscar a Mejor Película en 1994?", options: ["Forrest Gump", "Pulp Fiction", "The Shawshank Redemption", "El Rey León"], answer: "Forrest Gump" },
      { question: "¿Quién dirigió la trilogía de El Señor de los Anillos?", options: ["Steven Spielberg", "James Cameron", "Peter Jackson", "George Lucas"], answer: "Peter Jackson" },
      { question: "¿Cuántos jugadores hay en un equipo de fútbol (en el campo)?", options: ["9", "10", "11", "12"], answer: "11" },
      { question: "¿Quién ganó el Mundial de fútbol en 2022?", options: ["Brasil", "Francia", "Argentina", "Croacia"], answer: "Argentina" },
      { question: "¿Cuál es el país más grande del mundo en superficie?", options: ["Estados Unidos", "China", "Canadá", "Rusia"], answer: "Rusia" },
      { question: "¿Cuál es el idioma más hablado del mundo (nativos)?", options: ["Inglés", "Mandarín", "Español", "Árabe"], answer: "Mandarín" },
      { question: "¿Qué país inventó el papel?", options: ["India", "Egipto", "China", "Grecia"], answer: "China" },
      { question: "¿En qué ciudad está ubicada la Torre Eiffel?", options: ["Londres", "Madrid", "París", "Roma"], answer: "París" },
      { question: "¿Cuál es el océano más grande del mundo?", options: ["Atlántico", "Índico", "Pacífico", "Ártico"], answer: "Pacífico" },
      { question: "¿Quién pintó la Mona Lisa?", options: ["Picasso", "Van Gogh", "Leonardo da Vinci", "Michelangelo"], answer: "Leonardo da Vinci" },
      { question: "¿En qué año se llegó por primera vez a la Luna?", options: ["1969", "1959", "1979", "1989"], answer: "1969" }
    ];

    let current = 0;
    let score = 0;

    function showQuestion() {
      const q = questions[current];
      document.getElementById('question').textContent = q.question;
      const optionsDiv = document.getElementById('options');
      optionsDiv.innerHTML = '';
      q.options.forEach(opt => {
        const btn = document.createElement('button');
        btn.textContent = opt;
        btn.onclick = () => checkAnswer(opt);
        optionsDiv.appendChild(btn);
      });
      document.getElementById('feedback').textContent = '';
      updateProgress();
    }

    function checkAnswer(selected) {
      const correct = questions[current].answer;
      const feedback = document.getElementById('feedback');
      if (selected === correct) {
        feedback.textContent = '🎉 ¡Correcto!';
        feedback.style.color = 'green';
        score++;
      } else {
        feedback.textContent = `❌ Incorrecto. La respuesta correcta es: ${correct}`;
        feedback.style.color = 'red';
      }
      document.getElementById('score').textContent = `Puntaje: ${score}`;
      current++;
      if (current < questions.length) {
        setTimeout(showQuestion, 1800);
      } else {
        setTimeout(() => {
          document.querySelector('.trivia-container').innerHTML = `
            <h2>🎊 ¡Juego terminado! 🎊</h2>
            <p>Tu puntaje final es: <strong>${score}</strong> de <strong>${questions.length}</strong></p>
            <button onclick="location.reload()" style="padding:10px 20px; font-size:1rem; border:none; background:#74aee9; color:white; border-radius:10px; cursor:pointer;">Volver a jugar</button>
          `;
        }, 1800);
      }
    }

    function updateProgress() {
      const progress = document.getElementById('progress-fill');
      const percent = ((current) / questions.length) * 100;
      progress.style.width = percent + '%';
    }

    showQuestion();
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title>Matematika O‘yini</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      padding: 50px;
      background-color: #f5f5f5;
    }
    .box {
      background: #fff;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      display: inline-block;
    }
    input {
      padding: 10px;
      font-size: 16px;
      width: 100px;
      text-align: center;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      margin-top: 10px;
      cursor: pointer;
    }
    .result, .timer, .score {
      margin-top: 20px;
      font-size: 18px;
    }
    .final {
      font-weight: bold;
      font-size: 22px;
      color: green;
    }
  </style>
</head>
<body>

  <div class="box">
    <h2>🧠 Oddiy Matematika O‘yini</h2>
    <div id="question">Savol yuklanmoqda...</div>
    <input type="number" id="answer" placeholder="Javob" autocomplete="off">
    <br>
    <button onclick="checkAnswer()">Tekshirish</button>
    <div class="timer" id="timer">⏱ Vaqt: 10</div>
    <div class="result" id="result"></div>
    <div class="score" id="score">Ball: 0 / 0</div>
    <div class="final" id="final"></div>
  </div>

  <script>
    let num1, num2, operator, correctAnswer;
    let score = 0;
    let questionCount = 0;
    const totalQuestions = 10;
    let timeLeft = 10;
    let timerInterval;

    function generateQuestion() {
      if (questionCount >= totalQuestions) {
        endGame();
        return;
      }

      questionCount++;
      num1 = Math.floor(Math.random() * 10) + 1;
      num2 = Math.floor(Math.random() * 10) + 1;
      operator = Math.random() > 0.5 ? '+' : '-';
      correctAnswer = operator === '+' ? num1 + num2 : num1 - num2;

      document.getElementById("question").innerText = `Savol ${questionCount}: ${num1} ${operator} ${num2} = ?`;
      document.getElementById("answer").value = '';
      document.getElementById("result").innerText = '';
      document.getElementById("score").innerText = `Ball: ${score} / ${questionCount - 1}`;
      startTimer();
    }

    function checkAnswer() {
      clearInterval(timerInterval);
      let userAnswer = parseInt(document.getElementById("answer").value);
      if (userAnswer === correctAnswer) {
        document.getElementById("result").innerText = "✅ To‘g‘ri!";
        score++;
      } else {
        document.getElementById("result").innerText = `❌ Xato! To‘g‘ri javob: ${correctAnswer}`;
      }
      document.getElementById("score").innerText = `Ball: ${score} / ${questionCount}`;
      setTimeout(generateQuestion, 1500);
    }

    function startTimer() {
      timeLeft = 10;
      document.getElementById("timer").innerText = `⏱ Vaqt: ${timeLeft}`;
      timerInterval = setInterval(() => {
        timeLeft--;
        document.getElementById("timer").innerText = `⏱ Vaqt: ${timeLeft}`;
        if (timeLeft <= 0) {
          clearInterval(timerInterval);
          document.getElementById("result").innerText = `⌛ Vaqt tugadi! To‘g‘ri javob: ${correctAnswer}`;
          document.getElementById("score").innerText = `Ball: ${score} / ${questionCount}`;
          setTimeout(generateQuestion, 1500);
        }
      }, 1000);
    }

    function endGame() {
      document.getElementById("question").innerText = "🏁 O‘yin tugadi!";
      document.getElementById("timer").innerText = '';
      document.getElementById("result").innerText = '';
      document.getElementById("final").innerText = `Siz ${totalQuestions} savoldan ${score} tasiga to‘g‘ri javob berdingiz!`;
      document.getElementById("answer").style.display = "none";
    }

    // O'yinni boshlash
    generateQuestion();
  </script>

</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Clazora – Class 8 Hub</title>

  <!-- ✅ SEO and Mobile Meta Tags -->
  <meta name="description" content="Clazora – A class hub for Class 8 with homework, study materials, announcements, quizzes, and chat.">
  <meta name="keywords" content="Clazora, Class 8, School, Homework, Study, Students, Daffodils Public School, Class Hub">
  <meta name="author" content="Aditya Singh, Alok Tiwari">
  <meta name="robots" content="index, follow">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="canonical" href="https://yourusername.github.io/clazora/" />

  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background-color: #f9f9f9;
      color: #333;
    }
    header {
      background-color: #3f51b5;
      color: white;
      padding: 20px;
      text-align: center;
    }
    section {
      padding: 20px;
      border-bottom: 1px solid #ccc;
      background: white;
    }
    h2 {
      color: #3f51b5;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }
    th, td {
      padding: 10px;
      border: 1px solid #aaa;
    }
    textarea, input[type="text"] {
      width: 100%;
      padding: 8px;
      margin-top: 5px;
    }
    button {
      margin-top: 5px;
      padding: 6px 12px;
      background: #3f51b5;
      color: white;
      border: none;
      cursor: pointer;
    }
    ul {
      padding-left: 20px;
    }
    img {
      margin: 10px;
      border-radius: 5px;
      width: 200px;
    }
    footer {
      text-align: center;
      background: #ddd;
      padding: 10px;
    }
  </style>
</head>
<body>

  <header>
    <h1>Clazora – Class 8 Hub</h1>
    <p>Our Class, Our Hub – Stay Organized, Learn Together</p>
  </header>

  <section id="schedule">
    <h2>📅 Class Schedule</h2>
    <table>
      <tr><th>Day</th><th>Subjects</th></tr>
      <!-- Add your schedule rows here -->
    </table>
  </section>

  <section id="materials">
    <h2>📚 Study Materials</h2>
    <ul>
      <!-- Add material links here -->
    </ul>
  </section>

  <section id="homework">
    <h2>📝 Homework Tracker</h2>
    <ul id="hw-list"></ul>
    <div class="auth-only" style="display:none;">
      <input type="text" id="hw-input" placeholder="Add new homework...">
      <button onclick="addHomework()">Add Homework</button>
    </div>
  </section>

  <section id="announcements">
    <h2>📢 Announcements</h2>
    <ul id="announcement-list"></ul>
    <div class="auth-only" style="display:none;">
      <input type="text" id="announcement-input" placeholder="Add announcement...">
      <button onclick="addAnnouncement()">Add Announcement</button>
    </div>
  </section>

  <section id="quiz">
    <h2>🧠 Class Quiz</h2>
    <div id="quiz-box">
      <p id="quiz-question">No quiz yet.</p>
      <div id="quiz-options"></div>
      <p id="quiz-result"></p>
    </div>
    <div class="auth-only" style="display:none;">
      <input type="text" id="quiz-question-input" placeholder="Enter your quiz question...">
      <input type="text" id="quiz-option1" placeholder="Option 1 (Correct)">
      <input type="text" id="quiz-option2" placeholder="Option 2">
      <button onclick="addQuiz()">Add Quiz Question</button>
    </div>
  </section>

  <section id="chat">
    <h2>💬 Class Chat</h2>
    <textarea id="chat-input" placeholder="Type your message..."></textarea>
    <button onclick="postMessage()">Send</button>
    <ul id="chat-messages"></ul>
  </section>

  <section id="creative">
    <h2>🎨 Creative Corner</h2>
    <!-- Add creative content here -->
  </section>

  <section id="gallery">
    <h2>📷 Photo Gallery</h2>
    <!-- Add image links or <img> tags here -->
  </section>

  <footer>
    <p>Made with ❤️ by Aditya Singh & Alok Tiwari for Daffodils Public School – Class 8 (2025)</p>
  </footer>

  <script>
    let isAuthorized = false;
    let userName = "";

    function loginUser() {
      userName = sessionStorage.getItem("username");
      if (!userName) {
        userName = prompt("Enter your name:");
        if (!userName || userName.trim() === "") {
          userName = "Anonymous";
        }
        sessionStorage.setItem("username", userName);
      }

      if (sessionStorage.getItem("authorized") === "true") {
        isAuthorized = true;
        document.querySelectorAll('.auth-only').forEach(el => el.style.display = "block");
        return;
      }

      const password = prompt("Enter the password to access full features:");
      if (password === "sparkbolt") {
        isAuthorized = true;
        sessionStorage.setItem("authorized", "true");
        alert("✅ Access granted. Welcome " + userName + "!");
        document.querySelectorAll('.auth-only').forEach(el => el.style.display = "block");
      } else {
        alert("❌ Incorrect password. You're in view-only mode.");
      }
    }

    function addHomework() {
      const input = document.getElementById("hw-input");
      const text = input.value.trim();
      if (text) {
        const li = document.createElement("li");
        li.textContent = text;
        document.getElementById("hw-list").appendChild(li);
        input.value = "";
      }
    }

    function addAnnouncement() {
      const input = document.getElementById("announcement-input");
      const text = input.value.trim();
      if (text) {
        const li = document.createElement("li");
        li.textContent = text;
        document.getElementById("announcement-list").appendChild(li);
        input.value = "";
      }
    }

    function postMessage() {
      const input = document.getElementById("chat-input");
      const message = input.value.trim();
      const list = document.getElementById("chat-messages");
      if (message) {
        const li = document.createElement("li");
        li.innerHTML = `<strong>${userName}:</strong> ${message}`;
        list.appendChild(li);
        input.value = "";
      }
    }

    let quizzes = [];

    function displayQuiz(index) {
      const quizBox = document.getElementById("quiz-box");
      const questionP = document.getElementById("quiz-question");
      const optionsDiv = document.getElementById("quiz-options");
      const resultP = document.getElementById("quiz-result");

      if (quizzes.length === 0) {
        questionP.textContent = "No quiz yet.";
        optionsDiv.innerHTML = "";
        resultP.textContent = "";
        return;
      }

      const quiz = quizzes[index];
      questionP.textContent = quiz.question;
      optionsDiv.innerHTML = "";
      resultP.textContent = "";

      quiz.options.forEach(option => {
        const btn = document.createElement("button");
        btn.textContent = option;
        btn.onclick = () => {
          if (option === quiz.answer) {
            resultP.textContent = "✅ Correct!";
            resultP.style.color = "green";
          } else {
            resultP.textContent = "❌ Wrong! Try again.";
            resultP.style.color = "red";
          }
        };
        optionsDiv.appendChild(btn);
      });
    }

    function addQuiz() {
      const question = document.getElementById("quiz-question-input").value.trim();
      const option1 = document.getElementById("quiz-option1").value.trim();
      const option2 = document.getElementById("quiz-option2").value.trim();

      if (question && option1 && option2) {
        quizzes.push({
          question: question,
          options: [option1, option2],
          answer: option1
        });

        document.getElementById("quiz-question-input").value = "";
        document.getElementById("quiz-option1").value = "";
        document.getElementById("quiz-option2").value = "";

        displayQuiz(quizzes.length - 1);
        alert("Quiz added!");
      } else {
        alert("Please fill in all quiz fields.");
      }
    }

    window.onload = () => {
      loginUser();
      displayQuiz(0);
    };
  </script>

</body>
</html>


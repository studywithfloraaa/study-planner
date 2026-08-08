<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Flora Academic Study Planner 🌸🩵</title>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600&family=Quicksand:wght@500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-color: #f4f8fb;
      --card-bg: #ffffff;
      --primary: #a8d8ea;
      --primary-dark: #72b6d3;
      --accent-pink: #fcd5ce;
      --accent-green: #d8e2dc;
      --text-color: #4a5568;
      --text-light: #718096;
      --shadow: 0 8px 20px rgba(168, 216, 234, 0.25);
      --radius: 20px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Quicksand', sans-serif;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-color);
      padding: 30px 20px;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    /* Floating Clouds Animation */
    @keyframes float {
      0% { transform: translateY(0px); }
      50% { transform: translateY(-8px); }
      100% { transform: translateY(0px); }
    }

    .container {
      max-width: 950px;
      width: 100%;
    }

    /* Header Section */
    header {
      text-align: center;
      margin-bottom: 25px;
      animation: float 4s ease-in-out infinite;
    }

    header h1 {
      font-family: 'Fredoka', sans-serif;
      color: var(--primary-dark);
      font-size: 2.2rem;
      margin-bottom: 5px;
    }

    header p {
      color: var(--text-light);
      font-size: 1rem;
    }

    /* Cute Progress Bar Card */
    .progress-card {
      background: var(--card-bg);
      border-radius: var(--radius);
      padding: 20px;
      box-shadow: var(--shadow);
      margin-bottom: 25px;
      border: 2px solid #e1eff6;
      text-align: center;
    }

    .progress-title {
      font-weight: 700;
      color: var(--text-color);
      margin-bottom: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 10px;
    }

    .progress-bar-bg {
      background-color: #eaf3f8;
      border-radius: 50px;
      height: 22px;
      width: 100%;
      overflow: hidden;
      position: relative;
    }

    .progress-bar-fill {
      background: linear-gradient(90deg, var(--primary) 0%, var(--primary-dark) 100%);
      height: 100%;
      width: 0%;
      border-radius: 50px;
      transition: width 0.5s ease-in-out;
    }

    /* Grid Layout */
    .planner-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
    }

    @media (max-width: 768px) {
      .planner-grid {
        grid-template-columns: 1fr;
      }
    }

    /* Card Styling */
    .card {
      background: var(--card-bg);
      border-radius: var(--radius);
      padding: 22px;
      box-shadow: var(--shadow);
      border: 2px solid #e8f1f5;
    }

    .card-title {
      font-family: 'Fredoka', sans-serif;
      font-size: 1.25rem;
      color: var(--primary-dark);
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    /* Input & Button Styling */
    .input-group {
      display: flex;
      gap: 8px;
      margin-bottom: 15px;
    }

    input[type="text"], input[type="number"] {
      width: 100%;
      padding: 10px 14px;
      border: 2px solid #e1eff6;
      border-radius: 12px;
      outline: none;
      font-size: 0.95rem;
      transition: all 0.3s;
    }

    input[type="text"]:focus, input[type="number"]:focus {
      border-color: var(--primary);
    }

    button.btn-add {
      background-color: var(--primary);
      color: white;
      border: none;
      border-radius: 12px;
      padding: 10px 18px;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    button.btn-add:hover {
      background-color: var(--primary-dark);
      transform: scale(1.03);
    }

    /* Task / Item Lists */
    ul {
      list-style: none;
    }

    li.item-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background-color: #f8fafc;
      padding: 10px 14px;
      border-radius: 12px;
      margin-bottom: 8px;
      border: 1px solid #edf2f7;
      transition: all 0.3s ease;
    }

    li.item-row.completed {
      background-color: #eef8f5;
      text-decoration: line-through;
      color: #a0aec0;
      border-color: #d1e7dd;
    }

    .item-left {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    input[type="checkbox"] {
      width: 18px;
      height: 18px;
      accent-color: var(--primary-dark);
      cursor: pointer;
    }

    .btn-delete {
      background: none;
      border: none;
      color: #fc8181;
      cursor: pointer;
      font-size: 1.1rem;
      font-weight: bold;
    }

    .btn-delete:hover {
      color: #e53e3e;
    }

    /* Badge */
    .badge {
      background-color: var(--accent-pink);
      color: #8c4a4a;
      padding: 4px 10px;
      border-radius: 20px;
      font-size: 0.8rem;
      font-weight: 700;
    }
  </style>
</head>
<body>

  <div class="container">
    <!-- Header -->
    <header>
      <h1>Flora Academic Study Planner 🌸🩵</h1>
      <p>Stay organized, track your progress, & study comfortably!</p>
    </header>

    <!-- Overall Animated Progress Card -->
    <div class="progress-card">
      <div class="progress-title">
        <span>✨ Today's Productivity Progress</span>
        <span id="progress-percent">0% Completed</span>
      </div>
      <div class="progress-bar-bg">
        <div class="progress-bar-fill" id="progress-fill"></div>
      </div>
    </div>

    <!-- Main Grid -->
    <div class="planner-grid">

      <!-- 1. Daily Study Tasks -->
      <div class="card">
        <div class="card-title">🗓️ Daily Study Tasks</div>
        <div class="input-group">
          <input type="text" id="task-input" placeholder="Add a study goal (e.g. Read Psych Ch. 1)...">
          <button class="btn-add" onclick="addTask()">Add</button>
        </div>
        <ul id="task-list">
          <!-- Sample Items -->
        </ul>
      </div>

      <!-- 2. Assignments & Deadlines -->
      <div class="card">
        <div class="card-title">📌 Upcoming Deadlines</div>
        <div class="input-group">
          <input type="text" id="deadline-input" placeholder="Assignment / Project name...">
          <button class="btn-add" style="background-color: var(--accent-pink); color: #8c4a4a;" onclick="addDeadline()">Add</button>
        </div>
        <ul id="deadline-list">
          <!-- Sample Items -->
        </ul>
      </div>

      <!-- 3. Grade & Score Tracker -->
      <div class="card">
        <div class="card-title">📊 Grade & Score Tracker</div>
        <div class="input-group">
          <input type="text" id="subject-input" placeholder="Subject Name..." style="flex: 2;">
          <input type="text" id="score-input" placeholder="Score (e.g. 45/50)" style="flex: 1;">
          <button class="btn-add" onclick="addGrade()">Save</button>
        </div>
        <ul id="grade-list">
          <!-- Sample Items -->
        </ul>
      </div>

      <!-- 4. Cozy Motivational Notes -->
      <div class="card">
        <div class="card-title">💭 Soft Reminders & Notes</div>
        <div class="input-group">
          <input type="text" id="note-input" placeholder="Write a cozy quote or note...">
          <button class="btn-add" style="background-color: var(--accent-green); color: #4a6b5d;" onclick="addNote()">Post</button>
        </div>
        <ul id="note-list">
          <!-- Sample Items -->
        </ul>
      </div>

    </div>
  </div>

  <script>
    // Initial Sample Data
    let tasks = [
      { text: "Review Theories of Personality", done: false },
      { text: "Outline Chapter 3 Research", done: true }
    ];

    let deadlines = [
      { text: "Psychology Quiz", done: false }
    ];

    let grades = [
      { subject: "Gen Psych", score: "48/50" }
    ];

    let notes = [
      "Take small steps every day. Rest is part of the process too! ☁️"
    ];

    function renderAll() {
      renderTasks();
      renderDeadlines();
      renderGrades();
      renderNotes();
      updateProgress();
    }

    // Update Animated Progress Bar
    function updateProgress() {
      const total = tasks.length + deadlines.length;
      if (total === 0) {
        document.getElementById('progress-fill').style.width = '0%';
        document.getElementById('progress-percent').innerText = '0% Completed';
        return;
      }

      const completedTasks = tasks.filter(t => t.done).length;
      const completedDeadlines = deadlines.filter(d => d.done).length;
      const completedTotal = completedTasks + completedDeadlines;

      const percentage = Math.round((completedTotal / total) * 100);

      document.getElementById('progress-fill').style.width = percentage + '%';
      document.getElementById('progress-percent').innerText = percentage + '% Completed ' + (percentage === 100 ? '🎉 Great Job!' : '✨');
    }

    // 1. Tasks Logic
    function renderTasks() {
      const list = document.getElementById('task-list');
      list.innerHTML = '';
      tasks.forEach((item, index) => {
        list.innerHTML += `
          <li class="item-row ${item.done ? 'completed' : ''}">
            <div class="item-left">
              <input type="checkbox" ${item.done ? 'checked' : ''} onchange="toggleTask(${index})">
              <span>${item.text}</span>
            </div>
            <button class="btn-delete" onclick="deleteTask(${index})">&times;</button>
          </li>
        `;
      });
    }

    function addTask() {
      const input = document.getElementById('task-input');
      if (input.value.trim() !== '') {
        tasks.push({ text: input.value, done: false });
        input.value = '';
        renderTasks();
        updateProgress();
      }
    }

    function toggleTask(index) {
      tasks[index].done = !tasks[index].done;
      renderTasks();
      updateProgress();
    }

    function deleteTask(index) {
      tasks.splice(index, 1);
      renderTasks();
      updateProgress();
    }

    // 2. Deadlines Logic
    function renderDeadlines() {
      const list = document.getElementById('deadline-list');
      list.innerHTML = '';
      deadlines.forEach((item, index) => {
        list.innerHTML += `
          <li class="item-row ${item.done ? 'completed' : ''}">
            <div class="item-left">
              <input type="checkbox" ${item.done ? 'checked' : ''} onchange="toggleDeadline(${index})">
              <span>${item.text}</span>
            </div>
            <button class="btn-delete" onclick="deleteDeadline(${index})">&times;</button>
          </li>
        `;
      });
    }

    function addDeadline() {
      const input = document.getElementById('deadline-input');
      if (input.value.trim() !== '') {
        deadlines.push({ text: input.value, done: false });
        input.value = '';
        renderDeadlines();
        updateProgress();
      }
    }

    function toggleDeadline(index) {
      deadlines[index].done = !deadlines[index].done;
      renderDeadlines();
      updateProgress();
    }

    function deleteDeadline(index) {
      deadlines.splice(index, 1);
      renderDeadlines();
      updateProgress();
    }

    // 3. Grade Tracker Logic
    function renderGrades() {
      const list = document.getElementById('grade-list');
      list.innerHTML = '';
      grades.forEach((item, index) => {
        list.innerHTML += `
          <li class="item-row">
            <span><strong>${item.subject}:</strong> ${item.score}</span>
            <button class="btn-delete" onclick="deleteGrade(${index})">&times;</button>
          </li>
        `;
      });
    }

    function addGrade() {
      const subInput = document.getElementById('subject-input');
      const scoreInput = document.getElementById('score-input');
      if (subInput.value.trim() !== '' && scoreInput.value.trim() !== '') {
        grades.push({ subject: subInput.value, score: scoreInput.value });
        subInput.value = '';
        scoreInput.value = '';
        renderGrades();
      }
    }

    function deleteGrade(index) {
      grades.splice(index, 1);
      renderGrades();
    }

    // 4. Notes Logic
    function renderNotes() {
      const list = document.getElementById('note-list');
      list.innerHTML = '';
      notes.forEach((text, index) => {
        list.innerHTML += `
          <li class="item-row" style="background-color: #fcf8f2;">
            <span>🌸 ${text}</span>
            <button class="btn-delete" onclick="deleteNote(${index})">&times;</button>
          </li>
        `;
      });
    }

    function addNote() {
      const input = document.getElementById('note-input');
      if (input.value.trim() !== '') {
        notes.push(input.value);
        input.value = '';
        renderNotes();
      }
    }

    function deleteNote(index) {
      notes.splice(index, 1);
      renderNotes();
    }

    // Initial Run
    renderAll();
  </script>
</body>
</html>

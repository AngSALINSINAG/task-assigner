<!DOCTYPE html>
<html>
<head>
  <title>Task Assignment</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 480px;
      margin: auto;
      padding: 15px;
      background: white;
      border-radius: 12px;
      border: 1px solid black;
    }
    h2, h3 {
      color: #4B0082;
      text-align: center;
    }
    label {
      display: block;
      margin-top: 10px;
      font-weight: bold;
    }
    input, select, textarea, button {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border-radius: 8px;
      border: 1px solid #ccc;
      box-sizing: border-box;
    }
    button {
      background-color: #4B0082;
      color: white;
      font-weight: bold;
      border: none;
      margin-top: 15px;
    }
    .task {
      background: #f9f9f9;
      padding: 10px;
      margin: 10px 0;
      border-radius: 8px;
      border-left: 5px solid #4B0082;
    }
    .completed {
      text-decoration: line-through;
      color: gray;
    }
  </style>
</head>
<body>

  <h2>📋 Task Assignment</h2>

  <label for="user">Select Your Name:</label>
  <select id="user" onchange="loadView()">
    <option value="">-- Select Name --</option>
    <option>John Rey Estiva</option>
    <option>Zyra Plazo</option>
    <option>Dulce Maria Abigail A. Jastio</option>
    <option>Jewel Base</option>
  </select>

  <div id="taskView" style="display:none">
    <h3>Your Tasks</h3>
    <div id="taskList"></div>
    <button onclick="clearCompleted()">🗑 Clear Completed</button>
  </div>

  <div id="assignTask" style="display:none">
    <h3>Assign a Task</h3>
    <label>Assign To:</label>
    <select id="assignTo">
      <option>John Rey Estiva</option>
      <option>Zyra Plazo</option>
      <option>Dulce Maria Abigail A. Jastio</option>
      <option>Jewel Base</option>
    </select>
    <label>Task Name:</label>
    <input type="text" id="taskName">
    <label>Date Issued:</label>
    <input type="date" id="dateIssued">
    <label>Deadline:</label>
    <input type="date" id="deadline">
    <label>Link (optional):</label>
    <input type="url" id="taskLink">
    <label>Other Details:</label>
    <textarea id="details" rows="3"></textarea>
    <button onclick="saveTask()">✅ Assign Task</button>
  </div>

  <script>
    const assignors = ["John Rey Estiva", "Dulce Maria Abigail A. Jastio"];

    function loadView() {
      const user = document.getElementById("user").value;
      document.getElementById("taskList").innerHTML = "";
      document.getElementById("taskView").style.display = user ? "block" : "none";
      document.getElementById("assignTask").style.display = assignors.includes(user) ? "block" : "none";
      renderTasks(user);
    }

    function saveTask() {
      const assignTo = document.getElementById("assignTo").value;
      const taskName = document.getElementById("taskName").value;
      const dateIssued = document.getElementById("dateIssued").value;
      const deadline = document.getElementById("deadline").value;
      const link = document.getElementById("taskLink").value;
      const details = document.getElementById("details").value;

      if (!taskName || !dateIssued || !deadline) {
        alert("Please fill in all required fields.");
        return;
      }

      const newTask = {
        taskName, dateIssued, deadline, link, details, completed: false
      };

      const currentTasks = JSON.parse(localStorage.getItem(assignTo) || "[]");
      currentTasks.push(newTask);
      localStorage.setItem(assignTo, JSON.stringify(currentTasks));

      alert("✅ Task assigned to " + assignTo);
      if (document.getElementById("user").value === assignTo) {
        renderTasks(assignTo);
      }

      // Clear form
      document.getElementById("taskName").value = "";
      document.getElementById("dateIssued").value = "";
      document.getElementById("deadline").value = "";
      document.getElementById("taskLink").value = "";
      document.getElementById("details").value = "";
    }

    function renderTasks(user) {
      const container = document.getElementById("taskList");
      const tasks = JSON.parse(localStorage.getItem(user) || "[]");

      container.innerHTML = tasks.map((task, index) => `
        <div class="task ${task.completed ? 'completed' : ''}">
          <b>${task.taskName}</b><br>
          <small><b>Issued:</b> ${task.dateIssued} | <b>Deadline:</b> ${task.deadline}</small><br>
          ${task.link ? `<a href="${task.link}" target="_blank">🔗 View Link</a><br>` : ''}
          <div><b>Details:</b> ${task.details}</div>
          <label>
            <input type="checkbox" onchange="toggleComplete('${user}', ${index})" ${task.completed ? 'checked' : ''}>
            Mark as completed
          </label>
        </div>
      `).join("");
    }

    function toggleComplete(user, index) {
      const tasks = JSON.parse(localStorage.getItem(user));
      tasks[index].completed = !tasks[index].completed;
      localStorage.setItem(user, JSON.stringify(tasks));
      renderTasks(user);
      alert("🔔 Task status updated.");
    }

    function clearCompleted() {
      const user = document.getElementById("user").value;
      let tasks = JSON.parse(localStorage.getItem(user));
      tasks = tasks.filter(t => !t.completed);
      localStorage.setItem(user, JSON.stringify(tasks));
      renderTasks(user);
    }
  </script>

</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login Page</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f9;
      text-align: center;
      padding: 50px;
    }
    .login-container {
      background: #fff;
      padding: 20px;
      margin: auto;
      max-width: 300px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      border-radius: 10px;
    }
    input[type="text"], input[type="password"] {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ddd;
      border-radius: 5px;
    }
    button {
      background: #007bff;
      color: white;
      padding: 10px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background: #0056b3;
    }
    .logout-button {
      background: #dc3545;
      margin-top: 20px;
    }
    .logout-button:hover {
      background: #b02a37;
    }
  </style>
</head>
<body>
  <div class="login-container">
    <h1>Login</h1>
    <form id="loginForm">
      <input type="text" id="username" placeholder="ชื่อผู้ใช้งาน" required>
      <input type="text" id="studentId" placeholder="รหัสนักศึกษา" required>
      <button type="submit">Login</button>
    </form>
    <p id="greeting" style="margin-top: 20px; font-size: 18px; color: green;"></p>
    <button id="logoutButton" class="logout-button" style="display: none;">Logout</button>
  </div>

  <script>
    const esp32IP = "192.168.0.172"; // IP Address ของ ESP32
    const googleScriptURL = "https://script.google.com/macros/s/AKfycbzrOHcxyWZ4F_b8ORD6wrY0FfsZejWkfQbMOxXigLd5AFxUGgt7TN__lEILmbwYS3gowA/exec"; // URL ของ Google Apps Script

    const form = document.getElementById("loginForm");
    const greeting = document.getElementById("greeting");
    const logoutButton = document.getElementById("logoutButton");

    form.addEventListener("submit", (e) => {
      e.preventDefault();
      const username = document.getElementById("username").value;
      const studentId = document.getElementById("studentId").value;

      // บันทึกข้อมูลไปยัง Google Sheets
      fetch(`${googleScriptURL}?username=${encodeURIComponent(username)}&studentId=${encodeURIComponent(studentId)}`)
        .then((response) => response.text())
        .then((result) => console.log(result))
        .catch((error) => console.error("Error saving to Google Sheets:", error));

      // แสดงข้อความต้อนรับ
      greeting.textContent = `ยินดีต้อนรับ, ${username} (${studentId})!`;
      form.style.display = "none";
      logoutButton.style.display = "block";

      // ส่งคำสั่งให้ Servo หมุน 360 องศา
      fetch(`http://${esp32IP}/control?position=360`)
        .then((response) => {
          if (response.ok) {
            console.log("Servo moved to 360 degrees!");
          } else {
            console.error("Failed to move servo:", response.statusText);
          }
        })
        .catch((error) => console.error("Error:", error));
    });

    logoutButton.addEventListener("click", () => {
      greeting.textContent = "";
      form.style.display = "block";
      logoutButton.style.display = "none";

      // ส่งคำสั่งให้ Servo หมุนกลับไปที่ 0 องศา
      fetch(`http://${esp32IP}/control?position=0`)
        .then((response) => {
          if (response.ok) {
            console.log("Servo moved to 0 degrees!");
          } else {
            console.error("Failed to move servo:", response.statusText);
          }
        })
        .catch((error) => console.error("Error:", error));
    });
  </script>
</body>
</html>

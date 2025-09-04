# TECH-FEST

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Vatsalya Public School - Tech Fest 2025</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <script>
    const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbxLS0Fajm2Hc3llysjAmthw10g4CP3F3NSo3BFLsM2VLzEFFQBWwdakLheeD0q8XhGulw/exec";

    async function saveRegistration(event) {
      event.preventDefault();
      const formData = {
        name: document.getElementById('name').value,
        school: document.getElementById('school').value,
        class: document.getElementById('class').value,
        phone: document.getElementById('phone').value,
        email: document.getElementById('email').value,
        event: document.getElementById('event').value
      };

      const response = await fetch(SCRIPT_URL, {
        method: "POST",
        body: JSON.stringify(formData),
        headers: { "Content-Type": "application/json" }
      });

      if (response.ok) {
        alert("✅ Registration saved in Google Sheet!");
        document.getElementById("registrationForm").reset();
      } else {
        alert("❌ Error saving registration.");
      }
    }

    function adminLogin() {
      const password = prompt("Enter Admin Password:");
      if (password === "shivin joshi") {
        showAdminPanel();
      } else {
        alert("❌ Incorrect Password");
      }
    }

    async function showAdminPanel() {
      document.getElementById("registrationSection").style.display = "none";
      document.getElementById("adminSection").style.display = "block";

      const response = await fetch(SCRIPT_URL);
      const registrations = await response.json();

      const tbody = document.getElementById("adminTableBody");
      tbody.innerHTML = "";
      registrations.forEach((reg, index) => {
        const row = `<tr class='border'>
          <td class='p-2'>${index + 1}</td>
          <td class='p-2'>${reg.name}</td>
          <td class='p-2'>${reg.school}</td>
          <td class='p-2'>${reg.class}</td>
          <td class='p-2'>${reg.phone}</td>
          <td class='p-2'>${reg.email}</td>
          <td class='p-2'>${reg.event}</td>
        </tr>`;
        tbody.innerHTML += row;
      });

      document.getElementById("totalCount").innerText = registrations.length;
    }
  </script>
</head>
<body class="bg-gray-100">
  <div class="max-w-3xl mx-auto bg-white shadow-2xl rounded-2xl p-8 mt-10">
    <h1 class="text-3xl font-bold text-center text-blue-600 mb-6">Vatsalya Public School<br>Tech Fest 2025</h1>
    <p class="text-center text-gray-600 mb-6">Register now for <b>Demo Bot Trails</b> & <b>E-Sport</b></p>

    <div id="registrationSection">
      <form id="registrationForm" onsubmit="saveRegistration(event)" class="space-y-4">
        <div>
          <label class="block font-semibold">Full Name</label>
          <input type="text" id="name" required class="w-full border p-2 rounded">
        </div>
        <div>
          <label class="block font-semibold">School Name</label>
          <input type="text" id="school" required class="w-full border p-2 rounded">
        </div>
        <div>
          <label class="block font-semibold">Class</label>
          <input type="text" id="class" required class="w-full border p-2 rounded">
        </div>
        <div>
          <label class="block font-semibold">Contact Number</label>
          <input type="tel" id="phone" required class="w-full border p-2 rounded">
        </div>
        <div>
          <label class="block font-semibold">Email</label>
          <input type="email" id="email" required class="w-full border p-2 rounded">
        </div>
        <div>
          <label class="block font-semibold">Select Event</label>
          <select id="event" required class="w-full border p-2 rounded">
            <option value="Demo Bot Trails">Demo Bot Trails</option>
            <option value="E-Sport">E-Sport</option>
          </select>
        </div>
        <button type="submit" class="w-full bg-blue-600 text-white py-2 rounded-xl hover:bg-blue-700">Submit Registration</button>
      </form>

      <button onclick="adminLogin()" class="mt-6 w-full bg-gray-700 text-white py-2 rounded-xl hover:bg-gray-900">Admin Login</button>
    </div>

    <div id="adminSection" style="display:none;">
      <h2 class="text-2xl font-bold text-center text-red-600 mb-4">Admin Dashboard</h2>
      <p class="text-center mb-4">Total Participants: <b id="totalCount">0</b></p>
      <table class="w-full border text-sm">
        <thead>
          <tr class="bg-gray-200 border">
            <th class="p-2">#</th>
            <th class="p-2">Name</th>
            <th class="p-2">School</th>
            <th class="p-2">Class</th>
            <th class="p-2">Phone</th>
            <th class="p-2">Email</th>
            <th class="p-2">Event</th>
          </tr>
        </thead>
        <tbody id="adminTableBody"></tbody>
      </table>
    </div>
  </div>
</body>
</html>

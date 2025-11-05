# Non-AI-Project-1---Student-Fee-Management-System
A web-based Student Fee Management System for managing student details, payments, and fee records. Created as Non-AI Project 1 (Web version).

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Student Fee Management System</title>
  <style>
    body {
      font-family: "Segoe UI", sans-serif;
      background: #f3f6fa;
      margin: 0;
      padding: 0;
      color: #333;
    }

    header {
      background-color: #004aad;
      color: white;
      text-align: center;
      padding: 20px 0;
      font-size: 1.8em;
      letter-spacing: 1px;
    }

    .container {
      max-width: 900px;
      margin: 30px auto;
      background: white;
      border-radius: 12px;
      padding: 30px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
    }

    h2 {
      color: #004aad;
      text-align: center;
    }

    form {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
      margin-top: 20px;
    }

    label {
      font-weight: 600;
      margin-bottom: 5px;
      display: block;
    }

    input, select {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 1em;
    }

    button {
      grid-column: span 2;
      background: #004aad;
      color: white;
      border: none;
      padding: 12px;
      border-radius: 8px;
      font-size: 1em;
      cursor: pointer;
      transition: background 0.3s;
    }

    button:hover {
      background: #0066cc;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 30px;
    }

    th, td {
      padding: 12px;
      text-align: left;
      border-bottom: 1px solid #ddd;
    }

    th {
      background-color: #004aad;
      color: white;
    }

    tr:hover {
      background-color: #f1f1f1;
    }

    footer {
      text-align: center;
      padding: 15px;
      background-color: #004aad;
      color: white;
      margin-top: 40px;
      font-size: 0.95em;
      letter-spacing: 0.5px;
      border-radius: 0 0 12px 12px;
    }

    .actions button {
      background: #e53935;
      border: none;
      color: white;
      padding: 6px 10px;
      border-radius: 6px;
      cursor: pointer;
    }

    .actions button:hover {
      background: #c62828;
    }
  </style>
</head>
<body>
  <header>
    Student Fee Management System
  </header>

  <div class="container">
    <h2>Add Student Payment</h2>
    <form id="feeForm">
      <div>
        <label for="name">Student Name</label>
        <input type="text" id="name" placeholder="Enter student name" required>
      </div>
      <div>
        <label for="roll">Roll Number</label>
        <input type="text" id="roll" placeholder="Enter roll number" required>
      </div>
      <div>
        <label for="class">Class / Section</label>
        <input type="text" id="class" placeholder="e.g. 10-A" required>
      </div>
      <div>
        <label for="amount">Amount Paid (₹)</label>
        <input type="number" id="amount" placeholder="Enter fee amount" required>
      </div>
      <button type="submit">Add Record</button>
    </form>

    <h2>Fee Records</h2>
    <table id="feeTable">
      <thead>
        <tr>
          <th>Student Name</th>
          <th>Roll No</th>
          <th>Class</th>
          <th>Amount (₹)</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
      </tbody>
    </table>
  </div>

  <footer>
    Created by <strong>Shreyanjana Haldar</strong> | Sec-2A | Roll no.-72
  </footer>

  <script>
    const feeForm = document.getElementById('feeForm');
    const feeTableBody = document.querySelector('#feeTable tbody');
    let records = JSON.parse(localStorage.getItem('feeRecords')) || [];

    function renderTable() {
      feeTableBody.innerHTML = '';
      records.forEach((record, index) => {
        const row = document.createElement('tr');
        row.innerHTML = `
          <td>${record.name}</td>
          <td>${record.roll}</td>
          <td>${record.className}</td>
          <td>${record.amount}</td>
          <td class="actions"><button onclick="deleteRecord(${index})">Delete</button></td>
        `;
        feeTableBody.appendChild(row);
      });
      localStorage.setItem('feeRecords', JSON.stringify(records));
    }

    feeForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const name = document.getElementById('name').value.trim();
      const roll = document.getElementById('roll').value.trim();
      const className = document.getElementById('class').value.trim();
      const amount = document.getElementById('amount').value.trim();

      if (name && roll && className && amount) {
        records.push({ name, roll, className, amount });
        renderTable();
        feeForm.reset();
      }
    });

    function deleteRecord(index) {
      if (confirm('Are you sure you want to delete this record?')) {
        records.splice(index, 1);
        renderTable();
      }
    }

    renderTable();
  </script>
</body>
</html>

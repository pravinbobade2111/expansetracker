<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Expense Tracker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
    }

    input, button {
      margin: 5px;
    }

    table {
      margin: 20px auto;
      border-collapse: collapse;
      width: 80%;
    }

    th, td {
      border: 1px solid #ddd;
      padding: 8px;
      text-align: left;
    }
  </style>
</head>
<body>
  <h1>Expense Tracker</h1>

  <label for="projectName">Project Name:</label>
  <input type="text" id="projectName">
  
  <button onclick="chooseExperiment()">Choose Experiment</button>
  <button onclick="chooseDescription()">Choose Description</button>
  <button onclick="chooseCategory()">Choose Category</button>
  <button onclick="addExpenses()">Add Expenses</button>

  <table id="expenseTable">
    <thead>
      <tr>
        <th>Project Name</th>
        <th>Experiment</th>
        <th>Description</th>
        <th>Category</th>
        <th>Expenses</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody id="expenseTableBody">
      <!-- Data will be displayed here -->
    </tbody>
  </table>

  <script>
    function chooseExperiment() {
      let projectName = document.getElementById('projectName').value;
      let experiment = prompt('Enter experiment:');
      if (experiment) {
        addRow(projectName, experiment, '', '', '');
      }
    }

    function chooseDescription() {
      let projectName = document.getElementById('projectName').value;
      let description = prompt('Enter description:');
      if (description) {
        addRow(projectName, '', description, '', '');
      }
    }

    function chooseCategory() {
      let projectName = document.getElementById('projectName').value;
      let category = prompt('Enter category:');
      if (category) {
        addRow(projectName, '', '', category, '');
      }
    }

    function addExpenses() {
      let projectName = document.getElementById('projectName').value;
      let expenses = parseFloat(prompt('Enter expenses:'));
      if (!isNaN(expenses)) {
        addRow(projectName, '', '', '', expenses);
      }
    }

    function addRow(projectName, experiment, description, category, expenses) {
      let tableBody = document.getElementById('expenseTableBody');
      let newRow = tableBody.insertRow(-1);

      let cell1 = newRow.insertCell(0);
      let cell2 = newRow.insertCell(1);
      let cell3 = newRow.insertCell(2);
      let cell4 = newRow.insertCell(3);
      let cell5 = newRow.insertCell(4);
      let cell6 = newRow.insertCell(5);

      cell1.innerHTML = projectName;
      cell2.innerHTML = experiment;
      cell3.innerHTML = description;
      cell4.innerHTML = category;
      cell5.innerHTML = expenses;

      let editButton = document.createElement('button');
      editButton.innerHTML = 'Edit';
      editButton.onclick = function () {
        editRow(newRow);
      };

      let deleteButton = document.createElement('button');
      deleteButton.innerHTML = 'Delete';
      deleteButton.onclick = function () {
        tableBody.deleteRow(newRow.rowIndex);
      };

      cell6.appendChild(editButton);
      cell6.appendChild(deleteButton);
    }

    function editRow(row) {
      let cells = row.cells;
      document.getElementById('projectName').value = cells[0].innerHTML;
      let experiment = cells[1].innerHTML;
      let description = cells[2].innerHTML;
      let category = cells[3].innerHTML;
      let expenses = cells[4].innerHTML;

      if (experiment) {
        chooseExperiment();
      } else if (description) {
        chooseDescription();
      } else if (category) {
        chooseCategory();
      } else if (expenses) {
        addExpenses();
      }

      // After editing, remove the original row
      document.getElementById('expenseTableBody').removeChild(row);
    }
  </script>
</body>
</html>

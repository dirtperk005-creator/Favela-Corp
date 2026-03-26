# Favela-Corp
a website for uploading files 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Favela Corp</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #111;
      color: #fff;
      margin: 0;
    }

    header {
      background: #000;
      padding: 20px;
      text-align: center;
      font-size: 28px;
      font-weight: bold;
    }

    .container {
      padding: 20px;
      max-width: 800px;
      margin: auto;
    }

    input, textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border-radius: 5px;
      border: none;
    }

    button {
      padding: 10px 20px;
      background: #ff3c00;
      border: none;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }

    .card {
      background: #1c1c1c;
      padding: 15px;
      margin-top: 15px;
      border-radius: 10px;
    }
  </style>
</head>
<body>

<header>FAVELA CORP</header>

<div class="container">
  <h2>Upload Business Info</h2>

  <input type="text" id="name" placeholder="Business Name">
  <textarea id="description" placeholder="Business Description"></textarea>
  <input type="text" id="contact" placeholder="Contact Info">

  <button onclick="addBusiness()">Submit</button>

  <h2>Businesses</h2>
  <div id="businessList"></div>
</div>

<script>
  let businesses = JSON.parse(localStorage.getItem('businesses')) || [];

  function saveToStorage() {
    localStorage.setItem('businesses', JSON.stringify(businesses));
  }

  function renderBusinesses() {
    const list = document.getElementById('businessList');
    list.innerHTML = '';

    businesses.forEach((biz, index) => {
      list.innerHTML += `
        <div class="card">
          <h3>${biz.name}</h3>
          <p>${biz.description}</p>
          <small>Contact: ${biz.contact}</small><br>
          <button onclick="deleteBusiness(${index})">Delete</button>
        </div>
      `;
    });
  }

  function addBusiness() {
    const name = document.getElementById('name').value;
    const description = document.getElementById('description').value;
    const contact = document.getElementById('contact').value;

    if (!name || !description || !contact) {
      alert("Fill all fields!");
      return;
    }

    businesses.push({ name, description, contact });
    saveToStorage();
    renderBusinesses();

    document.getElementById('name').value = '';
    document.getElementById('description').value = '';
    document.getElementById('contact').value = '';
  }

  function deleteBusiness(index) {
    businesses.splice(index, 1);
    saveToStorage();
    renderBusinesses();
  }

  // Load saved data on page open
  renderBusinesses();
</script>

</body>
</html>
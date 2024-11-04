---
layout: page
---

<h1>Basic Form</h1>

<form id="basicForm">
  <label for="name">Name:</label><br>
  <input type="text" id="name" name="name"><br>
  <label for="email">Email:</label><br>
  <input type="email" id="email" name="email"><br><br>
  <input type="submit" value="Submit">
</form>

<script>
document.getElementById('basicForm').addEventListener('submit', function(event) {
  event.preventDefault();
  
  const webhookUrl = 'YOUR_WEBHOOK_URL_HERE';
  const formData = new FormData(event.target);
  const data = {};
  
  formData.forEach((value, key) => {
    data[key] = value;
  });

  fetch(webhookUrl, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
  })
  .then(response => response.json())
  .then(data => {
    console.log('Success:', data);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
});
</script>

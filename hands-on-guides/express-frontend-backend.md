### Step 1: Set Up Your Project

1. **Initialize your project**:
   ```bash
   mkdir express-frontend-backend
   cd express-frontend-backend
   npm init -y
   ```
   
2. **Install Express**:
   ```bash
   npm install express
   ```

3. **Create the necessary files**:
   ```bash
   touch index.js
   mkdir public
   touch public/index.html public/style.css public/script.js
   ```

### Step 2: Backend (Express.js)

In your `index.js` file, set up a basic Express server:

```javascript
// index.js

const express = require('express');
const app = express();
const port = 3000;

// Serve static files from the "public" directory
app.use(express.static('public'));

// Parse JSON body data
app.use(express.json());

// Handle POST requests to '/process'
app.post('/process', (req, res) => {
    const inputData = req.body.input;
    
    // Simple processing (e.g., reverse the input string)
    const processedData = inputData.split('').reverse().join('');
    
    // Send the processed data back to the frontend
    res.json({ result: processedData });
});

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});
```

### Step 3: Frontend (HTML, CSS, JavaScript)

**public/index.html**:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Express Frontend-Backend</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="app">
        <h1>Input Processor</h1>
        <input type="text" id="userInput" placeholder="Enter something..." />
        <button id="submitButton">Submit</button>
        <p>Processed Output: <span id="output"></span></p>
    </div>
    <script src="script.js"></script>
</body>
</html>
```

**public/style.css**:
```css
/* Simple styling */
body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f4f4f4;
}

#app {
    text-align: center;
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

input, button {
    padding: 10px;
    margin: 10px;
    font-size: 16px;
}
```

**public/script.js**:
```javascript
// Add event listener to the button
document.getElementById('submitButton').addEventListener('click', async () => {
    const userInput = document.getElementById('userInput').value;

    // Send the input to the backend
    const response = await fetch('/process', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ input: userInput })
    });

    const data = await response.json();

    // Display the processed data
    document.getElementById('output').textContent = data.result;
});
```

### Step 4: Run the Application

Start your Express server:

```bash
node index.js
```

Visit `http://localhost:3000` in your browser, and you should see the simple form. Enter some text, click the "Submit" button, and you'll see the processed output displayed on the page.

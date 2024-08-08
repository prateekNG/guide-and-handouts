## Let's Build a Typing Speed Test App! ⌨️🚀

This guide will help you create a Typing Speed Test app using HTML, CSS, and JavaScript. We'll break down the code into manageable components, making it easier to understand how everything works together.

### Phase 1: Setting Up the Foundation 🏗️

#### Step 1: Laying the Groundwork

**What we're doing:** We'll create the basic HTML structure for our Typing Speed Test app.

**Changes:**

1. **Create the Essential Files:**
    - `index.html`: Holds the content of our web page.
    - `styles.css`: Contains styles to enhance the page's visual appeal.
    - `app.js`: Houses the JavaScript code for interactivity.

2. **The Basic Structure:** Paste this code into `index.html`:

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Typing Speed Test</title>
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>
        <h1>Typing Speed Test</h1>
        <p id="quote">Click "Start" to begin the test.</p>
        <input type="text" id="input" placeholder="Start typing...">
        <button id="startButton">Start</button>
        <p id="result"></p>
        <script src="app.js"></script>
    </body>
    </html>
    ```

    This code sets up the following:
    - A heading (`<h1>`) for "Typing Speed Test".
    - A paragraph (`<p>`) to display the quote.
    - An input box (`<input>`) for users to type the quote.
    - A button (`<button>`) to start the test.
    - A paragraph (`<p>`) to display the result.
    - Links to our CSS file (`styles.css`) and JavaScript file (`app.js`).

#### Step 2: Adding a Splash of Colour! 🎨

**What we're doing:** We'll use CSS to style our app.

**Changes:**

1. **Style It Up:** Add the following CSS rules to `styles.css`:

    ```css
    body {
        font-family: Arial, sans-serif;
        text-align: center;
        background-color: #f0f0f0;
        margin: 0;
        padding: 0;
    }

    input, button {
        padding: 10px;
        font-size: 16px;
    }

    #quote {
        font-size: 24px;
        margin-bottom: 20px;
    }

    #result {
        font-size: 20px;
        color: green;
    }
    ```

    This CSS:
    - Sets a default font, background color, and centers text for the page.
    - Styles the heading, input box, button, and result paragraph.
    - Styles the quote with a larger font size.

### Phase 2: Breathing Life into Our App ✨

#### Step 1: Displaying a Random Quote 📜

**What we're doing:** We'll use JavaScript to display a random quote when the "Start" button is clicked.

**Changes:**

1. **Add the Quotes:** In `app.js`, add the following JavaScript code:

    ```javascript
    const quotes = [
        "The quick brown fox jumps over the lazy dog.",
        "JavaScript is fun!",
        "Practice makes perfect.",
        "Hello, world!"
    ];

    const quoteElement = document.getElementById('quote');
    const inputElement = document.getElementById('input');
    const startButton = document.getElementById('startButton');
    const resultElement = document.getElementById('result');

    let startTime, endTime;

    startButton.addEventListener('click', startTest);

    function startTest() {
        const randomIndex = Math.floor(Math.random() * quotes.length);
        quoteElement.textContent = quotes[randomIndex];
        inputElement.value = '';
        inputElement.disabled = false;
        inputElement.focus();
        startTime = new Date().getTime();
        resultElement.textContent = '';
    }
    ```

    This code:
    - Defines an array of quotes.
    - Selects the quote element, input element, start button, and result element from the HTML.
    - Adds an event listener to the start button to run the `startTest` function when clicked.
    - The `startTest` function displays a random quote, enables and focuses the input element, and records the start time.

#### Step 2: Calculating Typing Speed ⏱️

**What we're doing:** We'll calculate the typing speed once the user finishes typing the quote.

**Changes:**

1. **Measure Speed:** Add the following code to `app.js`:

    ```javascript
    inputElement.addEventListener('input', checkInput);

    function checkInput() {
        const quoteText = quoteElement.textContent;
        const inputText = inputElement.value;

        if (inputText === quoteText) {
            endTime = new Date().getTime();
            const timeTaken = (endTime - startTime) / 1000; // Time in seconds
            const wordsPerMinute = (quoteText.split(' ').length / timeTaken) * 60; // WPM
            resultElement.textContent = `You typed at ${Math.round(wordsPerMinute)} words per minute!`;
            inputElement.disabled = true;
        }
    }
    ```

    This code:
    - Adds an event listener to the input element to run the `checkInput` function on every input change.
    - The `checkInput` function compares the typed text with the quote.
    - If the text matches, it calculates the time taken, the words per minute, and displays the result.

### Conclusion 🎉

You now have a functioning Typing Speed Test app! 

**Possible Enhancements:**

- **Accuracy Calculation:** Calculate and display the typing accuracy.
- **Multiple Quotes:** Add more quotes for variety.
- **High Scores:** Save and display the highest typing speeds.

Keep exploring and enhancing your app to make it even more powerful and user-friendly!

---

### JavaScript Concepts Quick Reference:

Here's a checklist of JavaScript concepts used in the Typing Speed Test app:

| Concept                                    | Need                                                    | Explanation                                                                                           |
|---------------------------------------------|---------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| **DOM Selection (e.g., `getElementById`)** | Accessing HTML elements to manipulate them with JS      | Allows you to target specific elements like the input field, button, or quote.                     |
| **Event Listeners (e.g., `addEventListener`)** | Making elements interactive to user actions               | Makes the "Start" button and input field responsive to clicks and typing.                    |
| **DOM Manipulation (e.g., `textContent`)** | Dynamically updating HTML elements' content        | Used to display a random quote and the result dynamically.   |
| **Date Object (e.g., `new Date().getTime()`)**                 | Recording and calculating time     | Used to measure the time taken to type the quote.                                             |
| **String Methods (e.g., `split`, `length`)** | Manipulating and analyzing text     | Used to calculate words per minute from the typed quote. |

This checklist summarizes the key JavaScript concepts used to build the Typing Speed Test app. By understanding these concepts, you gain a foundation for creating interactive and dynamic web applications.

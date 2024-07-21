## Let's Build a To-Do List App! 📝

This guide will help you create a To-Do List app using HTML, CSS, and JavaScript. We'll break down the code into manageable components, making it easier to understand how everything works together.

### Phase 1: Setting Up the Foundation 🏗️

#### Step 1: Laying the Groundwork

**What we're doing:**  We'll create the basic HTML structure for our To-Do List app.

**Changes:**

1.  **Create the Essential Files:**
    -   `index.html`:  Holds the content of our web page.
    -   `styles.css`: Contains styles to enhance the page's visual appeal.
    -   `app.js`:  Houses the JavaScript code for interactivity.

2.  **The Basic Structure:** Paste this code into `index.html`:

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>To-Do List</title>
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>
        <h1>To-Do List</h1>
        <input type="text" id="taskInput" placeholder="Add a new task">
        <button id="addTaskButton">Add Task</button>
        <ul id="taskList"></ul>
        <script src="app.js"></script>
    </body>
    </html>
    ```

    This code sets up the following:
    -   A heading (`<h1>`) for "To-Do List".
    -   An input box (`<input>`) for users to enter tasks.
    -   A button (`<button>`) to add tasks.
    -   An unordered list (`<ul>`) to display tasks.
    -   Links to our CSS file (`styles.css`) and JavaScript file (`app.js`).

#### Step 2: Adding a Splash of Colour! 🎨

**What we're doing:** We'll use CSS to style our app.

**Changes:**

1.  **Style It Up:** Add the following CSS rules to `styles.css`:

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

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        background: #fff;
        margin: 5px 0;
        padding: 10px;
        border-radius: 5px;
        display: flex;
        align-items: center;
        width: 60%; 
        margin: 0 auto; 
    }

    .completed {
        text-decoration: line-through;
        color: gray;
    }

    li button {
        margin-left: auto; 
        padding: 8px 12px; 
        border: none; 
        border-radius: 4px; 
        cursor: pointer; 
    }

    li button + button { 
        margin-left: 10px; 
    }

    .completeButton {
        background-color: #4CAF50; 
        color: white;
    }

    .deleteButton {
        background-color: #f44336;
        color: white;
    }
    ```

    This CSS:
    -   Sets a default font, background color, and centers text for the page.
    -   Styles the heading, input box, button, and list items.
    -   Defines a `completed` class for completed tasks (strikethrough effect).
    -   Styles the "Complete" and "Delete" buttons with specific colors.

### Phase 2: Breathing Life into Our App ✨

#### Step 1: Let's Add Some Tasks! ✍️

**What we're doing:**  We'll use JavaScript to add tasks to our list.

**Changes:**

1.  **Listen Up!:**  In `app.js`, add the following JavaScript code:

    ```javascript
    const taskInput = document.getElementById('taskInput');
    const addTaskButton = document.getElementById('addTaskButton');
    const taskList = document.getElementById('taskList');

    addTaskButton.addEventListener('click', addTask);

    function addTask() {
        const taskText = taskInput.value;
        if (taskText === '') return; 

        const li = document.createElement('li');
        li.textContent = taskText;

        const completeButton = document.createElement('button');
        completeButton.textContent = 'Complete';
        completeButton.classList.add('completeButton');
        completeButton.addEventListener('click', completeTask); 

        const deleteButton = document.createElement('button');
        deleteButton.textContent = 'Delete';
        deleteButton.classList.add('deleteButton');
        deleteButton.addEventListener('click', deleteTask);

        li.appendChild(completeButton);
        li.appendChild(deleteButton);
        taskList.appendChild(li);
        taskInput.value = ''; 
    }
    ```

    This code:
    -   Selects the input box, add task button, and the task list from the HTML.
    -   Adds an event listener to the button, so when clicked, it runs the `addTask` function.
    -   The `addTask` function creates a new list item (`li`), sets its text content to the input value, creates and appends "Complete" and "Delete" buttons, and adds the `li` to the `taskList`. It also clears the input box.

#### Step 2:  Marking Tasks as Done ✅

**What we're doing:**  We'll add functionality to mark tasks as complete.

**Changes:**

1.  **Complete It!:**  Add the `completeTask` function to `app.js`:

    ```javascript
    function completeTask(event) {
        const li = event.target.parentElement;
        li.classList.toggle('completed');
    }
    ```

    This function:
    -   Finds the parent list item (`li`) of the clicked "Complete" button.
    -   Toggles the `completed` class on the `li` (adding or removing the strikethrough style).

#### Step 3: Deleting Tasks 🗑️

**What we're doing:**  Let's add functionality to delete tasks.

**Changes:**

1.  **Delete It!:**  Add the `deleteTask` function to `app.js`:

    ```javascript
    function deleteTask(event) {
        const li = event.target.parentElement; 
        li.remove(); 
    }
    ```

    This function:
    -   Gets the parent list item (`li`) of the clicked "Delete" button.
    -   Removes the `li` from the list.

### Phase 3: Remembering Our Tasks 🧠

#### Step 1: Saving Tasks for Later 💾

**What we're doing:** We'll use the browser's Local Storage to save tasks persistently.

**Changes:**

1.  **Save It!:**  Add the `saveTasks` function and update the `addTask`, `completeTask`, and `deleteTask` functions to call `saveTasks`:

    ```javascript
    function saveTasks() {
        const tasks = [];
        taskList.querySelectorAll('li').forEach(li => {
            tasks.push({
                text: li.firstChild.textContent,
                completed: li.classList.contains('completed')
            });
        });
        localStorage.setItem('tasks', JSON.stringify(tasks)); 
    }

    // Update the following functions to call saveTasks()
    function addTask() {
        // ... (previous code) ...
        saveTasks(); 
    }

    function completeTask(event) {
        // ... (previous code) ...
        saveTasks(); 
    }

    function deleteTask(event) {
        // ... (previous code) ...
        saveTasks();
    }
    ```

    -   `saveTasks` gathers task data and saves it to Local Storage.
    -   `addTask`, `completeTask`, and `deleteTask` now call `saveTasks` to update Local Storage after modifications.

#### Step 2: Loading Saved Tasks on Startup 🚀

**What we're doing:**  We'll load saved tasks from Local Storage when the page loads.

**Changes:**

1.  **Load It Up!:**  Add the `loadTasks` function and call it within a `DOMContentLoaded` event listener:

```javascript
document.addEventListener('DOMContentLoaded', loadTasks);

function loadTasks() {
    const tasks = JSON.parse(localStorage.getItem('tasks')) || []; 
    tasks.forEach(task => {
        const li = document.createElement('li');
        li.textContent = task.text;
        if (task.completed) {
            li.classList.add('completed'); 
        }

        const completeButton = document.createElement('button');
        completeButton.textContent = 'Complete';
        completeButton.classList.add('completeButton');
        completeButton.addEventListener('click', completeTask);

        const deleteButton = document.createElement('button');
        deleteButton.textContent = 'Delete';
        deleteButton.classList.add('deleteButton');
        deleteButton.addEventListener('click', deleteTask);

        li.appendChild(completeButton);
        li.appendChild(deleteButton); 

        taskList.appendChild(li); 
    });
}
```

-   `loadTasks` retrieves tasks from Local Storage and adds them to the task list.
-   The `DOMContentLoaded` event listener ensures `loadTasks` runs after the page fully loads.

### Conclusion 🎉

You now have a functioning To-Do List app! 

**Possible Enhancements:**

-   **Task Editing:**  Allow editing of existing tasks.
-   **Task Categorization:**  Implement categories for better organization.
-   **Search Functionality:**  Add a search bar to filter tasks.
-   **Due Dates:**  Include due date functionality for tasks.

Keep exploring and enhancing your app to make it even more powerful and user-friendly!

---

### JavaScript Concepts Quick Reference:

Here's a checklist of JavaScript concepts used in the To-Do List app:

| Concept                                    | Need                                                    | Explanation                                                                                           |
|---------------------------------------------|---------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| **DOM Selection (e.g., `getElementById`)** | Accessing HTML elements to manipulate them with JS      | Allows you to target specific elements like the input field, button, or list.                     |
| **Event Listeners (e.g., `addEventListener`)** | Making elements interactive to user actions               | Makes the "Add Task," "Complete," and "Delete" buttons responsive to clicks.                    |
| **DOM Manipulation (e.g., `createElement`, `appendChild`)** | Dynamically creating and adding HTML elements        | Used to create new list items (`<li>`) with buttons and add them to the task list dynamically.   |
| **`textContent` Property**                 | Getting or setting the text content of an element     | Used to display the task text within each list item.                                             |
| **`classList` (e.g., `add`, `toggle`, `contains`)** | Adding, removing, and checking for CSS classes     | Manages the "completed" class for styling completed tasks.                                    |
| **Event Object (e.g., `event.target`)**      | Accessing information about the event that occurred     | Used to identify which button was clicked (Complete or Delete) and its associated list item. |
| **Local Storage (e.g., `localStorage.setItem`, `localStorage.getItem`)** | Persisting data in the user's browser           | Allows the app to save tasks even after the browser window is closed.                              |
| **`JSON.stringify` and `JSON.parse`**       | Converting data to and from JSON format                 | Used to store and retrieve the task data in Local Storage.                                       |
| **`DOMContentLoaded` Event**               | Ensuring the script runs after the HTML is fully loaded | Guarantees that the task list is loaded from Local Storage when the page is ready.              |

This checklist summarizes the key JavaScript concepts used to build the To-Do List app. By understanding these concepts, you gain a foundation for creating interactive and dynamic web applications. 

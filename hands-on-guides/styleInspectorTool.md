### Guide: Building a Dynamic Style Inspector Tool

**Objective:** Build a Dynamic Style Inspector Tool that allows users to click on any element on a web page and see its computed styles. This activity will help understand CSS cascading, specificity, computed styles, and how to manipulate DOM elements using JavaScript.

---

## Step 1: Introduction

### Concepts to Understand:
1. **CSS Cascading**: How CSS rules are applied in a hierarchy.
2. **Specificity**: How the importance of CSS selectors is calculated.
3. **Computed Styles**: The final values of all CSS properties after all calculations are done.

### Activity Overview:
We will create a tool that:
- Highlights an element when clicked.
- Displays the computed styles of the clicked element.
- Allows users to interactively explore and modify the styles.

---

## Step 2: Setting Up the Project

### 1. Create a Basic HTML Template
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic Style Inspector Tool</title>
  <link rel="stylesheet" href="styles.css">
  <style>
    .box {
      width: 200px;
      height: 100px;
      background-color: lightblue;
      padding: 20px;
      margin: 10px;
    }
  </style>
</head>
<body>
  <div class="box" id="box1">Box 1</div>
  <div class="box" id="box2" style="background-color: lightcoral;">Box 2</div>
  <script src="script.js"></script>
</body>
</html>
```

### 2. Add External Stylesheet (styles.css)
```css
body {
  font-family: Arial, sans-serif;
  margin: 20px;
}

.box {
  border: 2px solid black;
}
```

---

## Step 3: Creating the Inspector Overlay

### 1. Create the Overlay Element
```javascript
const overlay = document.createElement('div');
overlay.style.position = 'absolute';
overlay.style.backgroundColor = 'rgba(255, 255, 0, 0.5)';
overlay.style.pointerEvents = 'none';
document.body.appendChild(overlay);
```

### 2. Capture Click Events and Highlight Element
```javascript
document.addEventListener('click', (event) => {
  const element = event.target;
  const rect = element.getBoundingClientRect();
  overlay.style.width = rect.width + 'px';
  overlay.style.height = rect.height + 'px';
  overlay.style.top = rect.top + 'px';
  overlay.style.left = rect.left + 'px';
});
```

---

## Step 4: Displaying Computed Styles

### 1. Retrieve Computed Styles
```javascript
document.addEventListener('click', (event) => {
  const element = event.target;
  const rect = element.getBoundingClientRect();
  overlay.style.width = rect.width + 'px';
  overlay.style.height = rect.height + 'px';
  overlay.style.top = rect.top + 'px';
  overlay.style.left = rect.left + 'px';

  const computedStyles = window.getComputedStyle(element);
  console.log(computedStyles);
});
```

### 2. Create a Style Viewer Panel
```html
<div id="styleViewer" style="position: fixed; right: 0; top: 0; width: 300px; height: 100%; background: white; border-left: 1px solid #ccc; overflow-y: auto; padding: 10px;"></div>
```

### 3. Populate the Style Viewer
```javascript
function displayStyles(styles) {
  const styleViewer = document.getElementById('styleViewer');
  styleViewer.innerHTML = '';
  for (let property of styles) {
    const value = styles.getPropertyValue(property);
    const styleItem = document.createElement('div');
    styleItem.textContent = `${property}: ${value}`;
    styleViewer.appendChild(styleItem);
  }
}

document.addEventListener('click', (event) => {
  const element = event.target;
  const rect = element.getBoundingClientRect();
  overlay.style.width = rect.width + 'px';
  overlay.style.height = rect.height + 'px';
  overlay.style.top = rect.top + 'px';
  overlay.style.left = rect.left + 'px';

  const computedStyles = window.getComputedStyle(element);
  displayStyles(computedStyles);
});
```

---

## Step 5: Enhancing the Inspector

### 1. Filter Displayed Styles
```javascript
function displayStyles(styles) {
  const styleViewer = document.getElementById('styleViewer');
  styleViewer.innerHTML = '';
  for (let property of styles) {
    const value = styles.getPropertyValue(property);
    if (value !== '') { // Filter out default/empty values
      const styleItem = document.createElement('div');
      styleItem.textContent = `${property}: ${value}`;
      styleViewer.appendChild(styleItem);
    }
  }
}
```

### 2. Add Copy to Clipboard Functionality
```html
<button id="copyButton">Copy Styles</button>
```

```javascript
document.getElementById('copyButton').addEventListener('click', () => {
  const styleViewer = document.getElementById('styleViewer');
  const styles = styleViewer.textContent;
  navigator.clipboard.writeText(styles).then(() => {
    alert('Styles copied to clipboard');
  });
});
```

### 3. Implement Search Function
```html
<input type="text" id="searchInput" placeholder="Search styles">
```

```javascript
document.getElementById('searchInput').addEventListener('input', (event) => {
  const searchTerm = event.target.value.toLowerCase();
  const styleItems = document.querySelectorAll('#styleViewer div');
  styleItems.forEach(item => {
    if (item.textContent.toLowerCase().includes(searchTerm)) {
      item.style.display = 'block';
    } else {
      item.style.display = 'none';
    }
  });
});
```

---

## Step 6: Iterative Improvements

### 1. Live Editing of Styles
```javascript
document.querySelectorAll('#styleViewer div').forEach(item => {
  item.addEventListener('click', () => {
    const property = item.textContent.split(': ')[0];
    const newValue = prompt(`Enter new value for ${property}`);
    if (newValue) {
      document.querySelector('.highlighted').style[property] = newValue;
      displayStyles(window.getComputedStyle(document.querySelector('.highlighted')));
    }
  });
});
```

### 2. Saving and Loading Configurations
```javascript
// Save to local storage
localStorage.setItem('styles', JSON.stringify(computedStyles));

// Load from local storage
const savedStyles = JSON.parse(localStorage.getItem('styles'));
if (savedStyles) {
  // Apply saved styles
  Object.keys(savedStyles).forEach(property => {
    document.querySelector('.highlighted').style[property] = savedStyles[property];
  });
}
```

### 3. Implementing Dark Mode
```javascript
const darkModeButton = document.createElement('button');
darkModeButton.textContent = 'Toggle Dark Mode';
document.body.appendChild(darkModeButton);

darkModeButton.addEventListener('click', () => {
  document.body.classList.toggle('dark-mode');
});

<style>
  .dark-mode {
    background-color: #333;
    color: #fff;
  }

  .dark-mode #styleViewer {
    background: #444;
    color: #fff;
  }
</style>
```

---

## Step 7: Testing and Debugging

### 1. Cross-Browser Testing
- Test the tool on multiple browsers (Chrome, Firefox, Safari, Edge) to ensure compatibility.
- Adjust the CSS and JavaScript code for any browser-specific issues.

### 2. Common Issues and Solutions
- Handle cases where the computed style is `null` or `undefined`.
- Ensure the tool works for all types of elements (including nested and pseudo-elements).

---

## Step 8: Conclusion and Review

### 1. Summary of Key Learnings
- CSS cascading, specificity, and computed styles.
- DOM manipulation with JavaScript.
- Event handling and real-time updates.

### 2. Real-World Applications and Extensions
- Expand the tool to include more CSS properties.
- Integrate with browser developer tools for enhanced functionality.
- Share the tool with peers and gather feedback for further improvements.

### 3. Encouragement for Further Exploration
- Encourage students to explore additional features and improvements.
- Suggest integrating the tool with frameworks like React or Vue.js for a more advanced version.
- Invite students to share their customized versions and use cases.

---

This detailed guide provides a comprehensive hands-on activity that encapsulates the concepts learned in CSS cascading, specificity, and computed styles. It encourages iterative development, real-world application, and further exploration.

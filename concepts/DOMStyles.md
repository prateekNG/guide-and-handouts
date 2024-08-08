### DOM: Guide on CSS Cascading and Computed Styles 

#### CSS Cascading

**CSS Cascading** means deciding which CSS rules apply to an element when there are multiple rules that could apply. The browser considers several factors: origin, specificity, importance, and order of the rules.

1. **Origin**: Where the CSS comes from (browser default styles, user styles, author styles).
2. **Specificity**: How specific the selectors are. ID selectors are more specific than class selectors, which are more specific than element selectors.
3. **Importance**: `!important` rules have the highest priority.
4. **Order**: If rules have the same specificity and importance, the last one in the CSS file is applied.

### Hands-on Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CSS Cascading Example</title>
  <style>
    body {
      font-size: 16px;
    }
    .text {
      color: blue;
      font-size: 20px;
    }
    #special {
      color: red;
    }
    .important-text {
      color: green !important;
    }
  </style>
</head>
<body>
  <p class="text" id="special">This is a special paragraph.</p>
  <p class="text important-text">This is an important paragraph.</p>
</body>
</html>
```

- The first paragraph (`<p class="text" id="special">`) will be red because the ID selector (`#special`) is more specific than the class selector (`.text`).
- The second paragraph (`<p class="text important-text">`) will be green because `!important` overrides other rules, regardless of specificity.

### Computed Styles

**Computed Styles** are the final styles applied to an element after all CSS rules have been processed. These include styles from CSS files, inline styles, and browser defaults.

#### Why Use Computed Styles?

- **Debugging**: To understand which styles are actually applied to an element.
- **Dynamic Styles**: Allows JavaScript to dynamically access and manipulate the styles applied to an element.

#### Example of Using Computed Styles

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Computed Styles Example</title>
  <style>
    .box {
      width: 100px;
      height: 100px;
      background-color: lightblue;
    }
  </style>
</head>
<body>
  <div class="box" id="myBox">Box</div>

  <script>
    const box = document.getElementById('myBox');
    const computedStyles = window.getComputedStyle(box);

    console.log('Width:', computedStyles.width); // 100px
    console.log('Height:', computedStyles.height); // 100px
    console.log('Background Color:', computedStyles.backgroundColor); // lightblue
  </script>
</body>
</html>
```

### Browser, User, and Author Defined Styles

**Browser Styles**: Default styles applied by the web browser.

**User Styles**: Styles defined by the user of the web browser for accessibility or personal preference.

**Author Styles**: Styles defined by the web developer in the webpage's CSS files, inline styles, or `<style>` tags.

#### Example of All Three Styles

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Cascading Styles Example</title>
  <style>
    /* Author styles */
    p {
      color: blue;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <p id="example" class="example">This is an example paragraph.</p>

  <script>
    // User styles (simulated via JavaScript for this example)
    const userStyle = document.createElement('style');
    userStyle.innerHTML = `
      p {
        color: green !important; /* Higher priority due to !important */
        font-size: 16px; /* Lower priority */
      }
    `;
    document.head.appendChild(userStyle);
  </script>
</body>
</html>
```

In this example:
- Browser styles are the default styles.
- Author styles override browser styles.
- User styles (with `!important`) override author styles.

### Specificity Points

Specificity is calculated based on the type of selectors used:
- **Inline styles**: `a = 1` (1000 points)
- **ID selectors**: `b = 1` (100 points per ID)
- **Class selectors, attribute selectors, pseudo-classes**: `c = 1` (10 points each)
- **Type selectors and pseudo-elements**: `d = 1` (1 point each)

#### Example Calculations

- `div` (Type selector): Specificity: `0, 0, 0, 1`
- `#header` (ID selector): Specificity: `0, 1, 0, 0`
- `.example` (Class selector): Specificity: `0, 0, 1, 0`
- `div.example`: Specificity: `0, 0, 1, 1` (Type selector + Class selector)
- `#header .menu-item`: Specificity: `0, 1, 1, 0` (ID selector + Class selector)

### Why Direct Access Doesn't Work for All Styles

Direct access through `element.style.propertyName` only shows inline styles and not styles applied via external stylesheets, embedded stylesheets, or inherited styles. Computed styles provide the actual values applied to an element, including those from various sources.

### Example to Illustrate Computed Styles

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Computed Styles Example</title>
  <style>
    .box {
      width: 200px;
      height: 100px;
      background-color: lightblue;
      padding: 20px;
    }
  </style>
</head>
<body>
  <div class="box" id="myBox">This is a box.</div>

  <script>
    const box = document.getElementById('myBox');

    // Accessing styles directly
    console.log('Directly Accessed Width:', box.style.width); // Only shows inline style, empty here

    // Accessing computed styles
    const computedStyles = window.getComputedStyle(box);
    console.log('Computed Width:', computedStyles.width); // 240px (200px width + 40px padding)
    console.log('Computed Height:', computedStyles.height); // 140px (100px height + 40px padding)
    console.log('Computed Background Color:', computedStyles.backgroundColor); // lightblue
  </script>
</body>
</html>
```

In this example:
- `box.style.width` returns an empty string because no inline style is set.
- `window.getComputedStyle(box).width` returns `240px` because it includes the width defined in the CSS (`200px`) plus the padding (`20px` on each side, totaling `40px`).

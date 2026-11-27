
---
subject: JavaScript
topic: Browser and DOM
day: 07
part: 1
tags: [JavaScript, Browser-DOM, interview-notes]
---

# Day 07 · Browser and DOM (Part 1)

> Understanding the DOM and using JavaScript to select, modify, create, style, and remove HTML elements dynamically.

## 1. DOM (Document Object Model)

**Definition:** DOM is a programming interface that represents an HTML document as a tree of objects. JavaScript uses the DOM API to access and dynamically modify HTML elements.

**Important terms:**
- **Node:** An individual item in the DOM tree.
- **Element:** A node representing an HTML element (`h1`, `p`, `div`).
- **Document:** Browser's representation of the loaded HTML page.
- **DOM API:** Browser-provided JavaScript methods and properties for manipulating the DOM.

**Key points:**
- Browser converts HTML into a tree-like DOM structure.
- JavaScript can modify content, styles, attributes, and elements.
- JavaScript can also respond to user interactions.

## 2. Selecting HTML Elements

**Definition:** DOM selection methods allow JavaScript to find HTML elements using their IDs, classes, tag names, or CSS selectors.

### A. `getElementById()`

Selects an element using its unique ID.

**Syntax:**
```js
const heading = document.getElementById("heading");
```

- Returns one matching element or `null`.
- Does not require `#` before the ID.

### B. `querySelector()`

Selects the **first element** matching a CSS selector.

**Syntax:**
```js
const heading = document.querySelector("#heading");
const message = document.querySelector(".message");
const paragraph = document.querySelector("p");
```

**CSS selector syntax:**

| Selector | Meaning |
|---|---|
| `"#heading"` | Element with ID `heading` |
| `".message"` | Element with class `message` |
| `"p"` | First paragraph element |
| `"div p"` | Paragraph inside a div |
| `"input[type='text']"` | Text input element |

### C. `querySelectorAll()`

Selects all elements matching a CSS selector.

**Syntax:**
```js
const paragraphs = document.querySelectorAll(".message");

console.log(paragraphs.length);

paragraphs.forEach((paragraph) => {
    console.log(paragraph.textContent);
});
```

- Returns a static `NodeList`.
- Supports `forEach()`.
- Does not automatically update when matching elements are added or removed.

### D. `getElementsByClassName()` and `getElementsByTagName()`

Select elements using class names or tag names.

**Syntax:**
```js
const messages = document.getElementsByClassName("message");

const paragraphs = document.getElementsByTagName("p");

console.log(messages.length);
console.log(paragraphs.length);
```

- Both return a live `HTMLCollection`.
- Automatically updates when matching DOM elements change.

### Comparison: DOM Selection Methods

| Method | Return type | Result |
|---|---|---|
| `getElementById()` | Element or `null` | One ID match |
| `querySelector()` | Element or `null` | First CSS selector match |
| `querySelectorAll()` | Static NodeList | All CSS selector matches |
| `getElementsByClassName()` | Live HTMLCollection | All class matches |
| `getElementsByTagName()` | Live HTMLCollection | All tag matches |

**Interview point:** Difference between static `NodeList` and live `HTMLCollection` is a commonly asked DOM interview question.

## 3. Changing Element Content

Three important properties are used to read or modify element content.

### A. `textContent`

Gets or changes the text content of an element.

**Syntax:**
```js
const heading = document.querySelector("#heading");

console.log(heading.textContent);

heading.textContent = "Welcome to JavaScript";
```

- Treats assigned content as plain text.
- Does not parse HTML.
- Includes text from hidden descendants.

### B. `innerHTML`

Gets or changes the HTML markup inside an element.

**Syntax:**
```js
const container = document.querySelector("#container");

container.innerHTML = "<h2>Hello JavaScript</h2><p>Welcome!</p>";
```

- Parses the assigned string as HTML.
- Browser creates corresponding DOM elements.
- Can insert multiple HTML elements.

**⚠️ Note:** Never insert untrusted user input directly into `innerHTML`. It can cause Cross-Site Scripting (XSS), allowing malicious HTML or JavaScript to execute.

### C. `innerText`

Gets or changes the rendered, visible text of an element.

**Syntax:**
```js
const container = document.querySelector("#container");

console.log(container.innerText);
```

- Represents rendered text.
- Considers CSS visibility and layout.
- Does not include text from hidden descendants.

### Comparison: Content Properties

| Property | Purpose | Parses HTML? |
|---|---|---|
| `textContent` | Read/write text content | No |
| `innerText` | Read/write rendered text | No |
| `innerHTML` | Read/write HTML markup | Yes |

**Interview point:**
- Prefer `textContent` for ordinary text updates.
- Use `innerHTML` when HTML insertion is intentionally required and safe.

## 4. Changing Input Values

**Definition:** The `value` property reads or modifies the current value of form controls such as input fields.

**Syntax:**
```js
const username = document.querySelector("#username");

console.log(username.value);

username.value = "Arun";

console.log(username.value);
```

**Key points:**
- `textContent` → Text inside HTML elements.
- `value` → Current value entered into form controls.

## 5. Changing HTML Attributes

**Definition:** An HTML attribute provides additional information or configuration for an HTML element.

Important methods:

| Method | Purpose |
|---|---|
| `getAttribute()` | Reads an attribute |
| `setAttribute()` | Adds or updates an attribute |
| `hasAttribute()` | Checks whether an attribute exists |
| `removeAttribute()` | Removes an attribute |

**Syntax:**
```js
const image = document.querySelector("#profileImage");

// Read an attribute
console.log(image.getAttribute("src"));

// Change an attribute
image.setAttribute("src", "new.jpg");

// Check attribute existence
console.log(image.hasAttribute("alt"));

// Remove an attribute
image.removeAttribute("alt");
```

Common attributes can also be accessed directly as properties.

```js
image.src = "new.jpg";
image.alt = "New profile";
```

**Key point:** `getAttribute()` and `setAttribute()` explicitly work with HTML attribute values.

## 6. Changing CSS Styles

**Definition:** JavaScript can modify an element's inline CSS through its `style` property.

**Syntax:**
```js
const heading = document.querySelector("#heading");

heading.style.color = "blue";
heading.style.backgroundColor = "yellow";
heading.style.fontSize = "32px";
```

### CSS Naming Conversion

CSS uses `kebab-case`, whereas JavaScript style properties use `camelCase`.

| CSS Property | JavaScript Property |
|---|---|
| `background-color` | `backgroundColor` |
| `font-size` | `fontSize` |
| `border-radius` | `borderRadius` |
| `margin-top` | `marginTop` |

### Better Approach: `classList`

Instead of modifying multiple inline styles, define CSS classes and manipulate them using JavaScript.

**Syntax:**
```js
const heading = document.querySelector("#heading");

heading.classList.add("active");

console.log(heading.classList.contains("active"));

heading.classList.remove("active");

heading.classList.toggle("active");
```

**Important methods:**

| Method | Purpose |
|---|---|
| `add()` | Adds a class |
| `remove()` | Removes a class |
| `toggle()` | Adds if absent; removes if present |
| `contains()` | Checks whether a class exists |
| `replace()` | Replaces one class with another |

**Key point:** `classList` is useful for building interactive interfaces by dynamically adding and removing CSS classes.

## 7. Creating and Removing Elements

**Definition:** JavaScript can dynamically create new HTML elements, insert them into the DOM, and remove existing elements.

**Important methods:**

| Method | Purpose |
|---|---|
| `document.createElement()` | Creates a new HTML element |
| `append()` | Adds content at the end |
| `prepend()` | Adds content at the beginning |
| `remove()` | Removes an element |

**Syntax:**
```js
const studentList = document.querySelector("#studentList");

// Create element
const newStudent = document.createElement("li");

// Add text
newStudent.textContent = "Arun";

// Insert at the end
studentList.append(newStudent);

// Create another element
const anotherStudent = document.createElement("li");
anotherStudent.textContent = "Priya";

// Insert at the beginning
studentList.prepend(anotherStudent);

// Remove element
newStudent.remove();
```

**Key points:**
- `createElement()` creates an element but does not automatically insert it into the DOM.
- `append()` inserts at the end.
- `prepend()` inserts at the beginning.
- `remove()` removes the selected element.

## 8. DOM Children Property

**Definition:** The `children` property returns the child elements of an element as a live `HTMLCollection`.

**Syntax:**
```js
console.log(studentList.children.length);
```

- `children` → Returns child elements.
- `children.length` → Returns the number of child elements.

## 9. Important DOM Execution Point

JavaScript must execute after the HTML elements it needs to select have been parsed.

**Example:**
```html
<body>
    <h1 id="heading">Hello</h1>

    <script src="script.js"></script>
</body>
```

- Placing the script at the end of `<body>` ensures the preceding HTML elements exist when the script executes.

## Comparison Tables

### `textContent` vs `innerHTML` vs `innerText`

| Feature | textContent | innerHTML | innerText |
|---|---|---|---|
| Reads text | Yes | Returns markup | Yes |
| Writes text | Yes | Yes | Yes |
| Parses HTML | No | Yes | No |
| Includes hidden text | Yes | Returns markup | No |

### Static NodeList vs Live HTMLCollection

| Feature | Static NodeList | Live HTMLCollection |
|---|---|---|
| Automatically updates | No | Yes |
| Returned by | `querySelectorAll()` | `getElementsByClassName()`, `getElementsByTagName()` |
| Reflects later DOM changes | No | Yes |

### `textContent` vs `value`

| Property | Usage |
|---|---|
| `textContent` | Reads or changes element text |
| `value` | Reads or changes form control values |

## Interview Q&A

**1. What is DOM?**

DOM stands for Document Object Model. It represents an HTML document as a tree of objects that JavaScript can access and modify.

**2. Difference between `querySelector()` and `querySelectorAll()`?**

`querySelector()` returns the first matching element. `querySelectorAll()` returns all matching elements as a static NodeList.

**3. Difference between NodeList and HTMLCollection?**

A NodeList returned by `querySelectorAll()` is static. An HTMLCollection returned by `getElementsByClassName()` or `getElementsByTagName()` is live.

**4. Difference between `textContent` and `innerHTML`?**

`textContent` treats content as plain text, whereas `innerHTML` parses and inserts HTML markup.

**5. Difference between `innerText` and `textContent`?**

`innerText` represents rendered visible text, whereas `textContent` includes text from hidden descendants.

**6. Which property is used to get an input field's current value?**

The `value` property.

**7. How do you add and remove CSS classes dynamically?**

Use `element.classList.add()` and `element.classList.remove()`.

**8. What is the difference between `append()` and `prepend()`?**

`append()` inserts content at the end of an element, whereas `prepend()` inserts content at the beginning.

**9. What is XSS?**

Cross-Site Scripting (XSS) is a security vulnerability where malicious HTML or JavaScript can be injected and executed in a webpage.

**10. Does declaring a DOM element using `const` prevent its modification?**

No. `const` prevents reassignment of the variable, but its referenced DOM element's properties can still be modified.

## Quick Cheat Sheet

### DOM Selection
```js
document.getElementById("id");
document.querySelector("#id");
document.querySelectorAll(".class");
document.getElementsByClassName("class");
document.getElementsByTagName("p");
```

### Content Manipulation
```js
element.textContent;
element.innerHTML;
element.innerText;
element.value;
```

### Attribute Manipulation
```js
element.getAttribute("src");
element.setAttribute("src", "new.jpg");
element.hasAttribute("alt");
element.removeAttribute("alt");

element.src = "new.jpg";
element.alt = "New profile";
```

### CSS Manipulation
```js
element.style.color = "blue";
element.style.backgroundColor = "yellow";
element.style.fontSize = "32px";

element.classList.add("active");
element.classList.remove("active");
element.classList.toggle("active");
element.classList.contains("active");
element.classList.replace("old", "new");
```

### Element Creation and Removal
```js
document.createElement("li");
element.append(newElement);
element.prepend(newElement);
element.remove();
```

### DOM Properties
```js
element.children;
element.children.length;
element.textContent;
element.innerHTML;
element.innerText;
element.value;
```

### Important Interview Reminders

- `querySelector()` → First matching element.
- `querySelectorAll()` → All matching elements; static NodeList.
- `getElementsByClassName()` → Live HTMLCollection.
- `getElementsByTagName()` → Live HTMLCollection.
- `textContent` → Plain text, including hidden descendant text.
- `innerText` → Rendered visible text.
- `innerHTML` → HTML markup; be careful about XSS.
- `value` → Current form control value.
- `classList` → CSS class manipulation.
- `createElement()` → Creates an element.
- `append()` → Adds at the end.
- `prepend()` → Adds at the beginning.
- `remove()` → Removes an element.
- `children.length` → Counts child elements.
- `const` → Prevents reassignment, not DOM property modification.

---
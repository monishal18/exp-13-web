# EXP 13 – Simulate an Asynchronous Operation Using Promises in React

**NAME:** Monisha L

**REG NO:** 2305001019

---

## Aim

To develop a React application that simulates an asynchronous student-data operation using a JavaScript Promise, displays a loading message while the operation is in progress, and displays the result when the Promise is fulfilled.

## Objectives

- To understand the concept of a Promise in JavaScript.
- To create a Promise using `new Promise()`.
- To use `.then()` and `.catch()` to handle success and errors.
- To use React's `useState()` hook to manage application state.
- To display loading and result messages using conditional rendering.

## Program

### Step 1: Create a React Project

```bash
npm create vite@latest async-student
cd async-student
npm install
npm run dev
```

Select React as the framework and JavaScript as the variant.

### Step 2: App.jsx

```jsx
import { useState } from "react";
import "./App.css";

function fetchStudentData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const student = {
        name: "Monisha",
        department: "CSE",
        year: "III"
      };

      resolve(student);

      // To test rejection:
      // reject(new Error("Unable to fetch student data"));
    }, 3000);
  });
}

function App() {
  const [loading, setLoading] = useState(false);
  const [student, setStudent] = useState(null);
  const [error, setError] = useState("");

  const handleFetch = () => {
    setLoading(true);
    setStudent(null);
    setError("");

    fetchStudentData()
      .then((data) => {
        setStudent(data);
      })
      .catch((err) => {
        setError(err.message);
      })
      .finally(() => {
        setLoading(false);
      });
  };

  return (
    <div className="app">
      <h1>Student Data Fetch</h1>

      <button onClick={handleFetch} disabled={loading}>
        {loading ? "Fetching..." : "Fetch Student"}
      </button>

      {loading && (
        <p>Fetching student information...</p>
      )}

      {student && (
        <div className="result">
          <h2>Student Details</h2>
          <p>Student Name: {student.name}</p>
          <p>Department: {student.department}</p>
          <p>Year: {student.year}</p>
          <h3>Status: Data Loaded Successfully</h3>
        </div>
      )}

      {error && (
        <p className="error">Error: {error}</p>
      )}
    </div>
  );
}

export default App;
```

### Step 3: App.css

```css
.app {
  text-align: center;
  padding: 40px;
}

button {
  padding: 12px 25px;
  background-color: blue;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: darkblue;
}

button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.result {
  margin: 25px auto;
  padding: 20px;
  background-color: #e8f5e9;
  width: 350px;
  border-radius: 10px;
}

.error {
  color: red;
  font-weight: bold;
}
```

### Step 4: index.css

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f2f2f2;
}

h1 {
  color: darkblue;
}

h2 {
  color: darkgreen;
}
```

### Step 5: main.jsx

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

## Output

### 1. Successful Student Data Fetch
<img width="333" height="306" alt="image" src="https://github.com/user-attachments/assets/0bea4bc8-960e-417c-8935-3a40e86b0f51" />



### 2. Promise Rejection (Error Handling)

<img width="325" height="223" alt="image" src="https://github.com/user-attachments/assets/7b4ae4af-2e05-4e0a-a538-45e49c486530" />


## Result

Thus, a React application was successfully developed to simulate an asynchronous student-data operation using JavaScript Promises. The application displayed a loading message and handled successful completion and errors using `.then()`, `.catch()`, and `.finally()`.

---


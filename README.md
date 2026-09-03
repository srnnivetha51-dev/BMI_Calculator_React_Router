# Ex06 BMI Calculator
## Date: 31/08/2026

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM
app.js
```
import React, { useState } from "react";
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
import "./App.css";

// Home Page
function Home() {
  return (
    <div className="container">
      <h1>BMI Calculator</h1>
      <p>Calculate your Body Mass Index easily.</p>

      <Link to="/calculator">
        <button>Go to Calculator</button>
      </Link>
    </div>
  );
}

// Calculator Page
function Calculator() {
  const [weight, setWeight] = useState("");
  const [height, setHeight] = useState("");
  const [bmi, setBmi] = useState(null);
  const [category, setCategory] = useState("");

  const calculateBMI = () => {
    if (!weight || !height || weight <= 0 || height <= 0) {
      alert("Please enter valid weight and height.");
      return;
    }

    // Convert height from cm to metres
    const heightInMeters = height / 100;

    // BMI calculation
    const result = weight / (heightInMeters * heightInMeters);

    setBmi(result.toFixed(2));

    // BMI categorization
    if (result < 18.5) {
      setCategory("Underweight");
    } else if (result < 25) {
      setCategory("Normal weight");
    } else if (result < 30) {
      setCategory("Overweight");
    } else {
      setCategory("Obesity");
    }
  };

  return (
    <div className="container">
      <h1>BMI Calculator</h1>

      <div className="input-group">
        <label>Weight (kg)</label>
        <input
          type="number"
          placeholder="Enter your weight"
          value={weight}
          onChange={(e) => setWeight(e.target.value)}
        />
      </div>

      <div className="input-group">
        <label>Height (cm)</label>
        <input
          type="number"
          placeholder="Enter your height"
          value={height}
          onChange={(e) => setHeight(e.target.value)}
        />
      </div>

      <button onClick={calculateBMI}>
        Calculate BMI
      </button>

      {bmi && (
        <div className="result">
          <h2>Your BMI: {bmi}</h2>
          <h3>Category: {category}</h3>
        </div>
      )}

      <Link to="/">
        <button className="back-button">
          Back to Home
        </button>
      </Link>
    </div>
  );
}

// Main App
function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/calculator">Calculator</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/calculator" element={<Calculator />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```
app.css
```

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f2f2f2;
}

nav {
  background: #222;
  padding: 15px;
  text-align: center;
}

nav a {
  color: white;
  text-decoration: none;
  margin: 0 20px;
  font-size: 18px;
}

.container {
  width: 400px;
  margin: 70px auto;
  padding: 30px;
  background: white;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
}

.input-group {
  text-align: left;
  margin: 20px 0;
}

.input-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
}

.input-group input {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 16px;
}

button {
  padding: 12px 25px;
  border: none;
  border-radius: 6px;
  background: #333;
  color: white;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background: #555;
}

.result {
  margin-top: 25px;
  padding: 15px;
  background: #eee;
  border-radius: 8px;
}

.back-button {
  margin-top: 20px;
}

```


## OUTPUT
<img width="1918" height="649" alt="image" src="https://github.com/user-attachments/assets/0b8d529f-5711-48c1-bc5d-24488b5706ca" />

<img width="1918" height="720" alt="image" src="https://github.com/user-attachments/assets/ab887d42-b8cc-4ea1-879b-27178a1e4d92" />



## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.

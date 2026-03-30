# Retro Salary Tracker Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Create a Super Mario themed static HTML page that tracks real-time earnings with falling coins and tax calculations.

**Architecture:** Single-file HTML/CSS/JS application for easy hosting on GitHub Pages. Uses CSS for pixel art and Web Audio API for 8-bit sound effects.

**Tech Stack:** HTML5, Vanilla CSS (8-bit style), Vanilla JavaScript, Google Fonts (Press Start 2P).

---

### Task 1: Basic Structure & Typography

**Files:**
- Create: `index.html`

**Step 1: Create index.html with meta tags and Google Fonts**
```html
<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Retro Salary Tracker</title>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
    <style>
        body {
            background-color: #5C94FC; /* Mario Sky Blue */
            font-family: 'Press Start 2P', cursive;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            color: white;
            image-rendering: pixelated;
        }
    </style>
</head>
<body>
        <div class="input-group">
            <input type="number" id="salaryInput" placeholder="Bruto Salaris (PM)">
            <input type="number" id="hoursInput" placeholder="Uren per week" value="40">
        </div>
        <div id="controls">
            <button onclick="startTracker()">START</button>
            <button onclick="stopTracker()">STOP</button>
        </div>
</body>
</html>
```

**Step 2: Commit**
```bash
git add index.html
git commit -m "feat: initial structure and retro typography"
```

---

### Task 2: CSS Pixel Art (Question Box & Pipe)

**Files:**
- Modify: `index.html`

**Step 1: Add CSS for Box and Pipe**
```css
/* Update <style> block */
.stage {
    position: relative;
    width: 300px;
    height: 400px;
    background: transparent;
}
.question-box {
    width: 50px;
    height: 50px;
    background: #FFD700;
    border: 4px solid #000;
    position: absolute;
    top: 50px;
    left: 125px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 30px;
}
.mario-pipe {
    width: 100px;
    height: 120px;
    background: #43B047;
    border: 4px solid #000;
    position: absolute;
    bottom: 0;
    left: 100px;
}
```

**Step 2: Commit**
```bash
git add index.html
git commit -m "feat: add css pixel art components"
```

---

### Task 3: Salary Calculation Logic

**Files:**
- Modify: `index.html`

**Step 1: Add JS for Tax Calculation**
```javascript
/* Add <script> block before </body> */
const calculateNetPerSecond = (grossMonthly, weeklyHours) => {
    // Simplified Dutch Tax 2024 (Box 1)
    const annualGross = grossMonthly * 12;
    // ... tax logic ...
    const workHoursPerMonth = (weeklyHours * 52) / 12;
    const workingSecondsPerMonth = workHoursPerMonth * 3600; 
    return {
        grossPerSecond: (grossMonthly / workingSecondsPerMonth),
        netPerSecond: (annualNet / 12 / workingSecondsPerMonth)
    };
};
```

**Step 2: Commit**
```bash
git add index.html
git commit -m "feat: implement simplified dutch tax logic"
```

---

### Task 4: Animation & Counter

**Files:**
- Modify: `index.html`

**Step 1: Implement Coin Animation Loop**
```javascript
let startTime, intervalId;
let grossTotal = 0, netTotal = 0;

const startTracker = () => {
    const grossMonthly = parseFloat(document.getElementById('salaryInput').value);
    const weeklyHours = parseFloat(document.getElementById('hoursInput').value);
    const rates = calculateNetPerSecond(grossMonthly, weeklyHours);
    
    intervalId = setInterval(() => {
        grossTotal += rates.grossPerSecond;
        netTotal += rates.netPerSecond;
        updateUI();
        if (Math.random() > 0.8) spawnCoin();
    }, 1000);
}
```

**Step 2: Commit**
```bash
git add index.html
git commit -m "feat: add animation and live counters"
```

---

### Task 5: Audio & Final Polish

**Files:**
- Modify: `index.html`

**Step 1: Add Audio Context and Controls**
- Add Mute toggle.
- Add Start/Stop buttons.
- Final CSS polish for layout.

**Step 2: Commit**
```bash
git add index.html
git commit -m "feat: add sound effects and finalize layout"
```

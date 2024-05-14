# Telemedicine Game
Developed for the Business Operations Research Lab (BOBALAB) at Berkeley Haas School of Business, this interactive Hospital Simulator Game immerses players in the role of a doctor engaging in telemedicine at UCSF. 

## Overview
**Hospital Simulator Game** is a dynamic, web-based simulation designed for the Business Operations Research Lab (BOBALab) at the Berkeley Haas School of Business. Players step into the shoes of a UCSF doctor, tasked with diagnosing patients through telemedicine. This interactive game tests players' medical knowledge and decision-making under time constraints, reflecting the real-world pressures of healthcare professionals.

## Objective
The game aims to simulate the experience of a doctor during a shift, where players must accurately diagnose patients and effectively manage their time. The ultimate goal is to achieve the highest score by making correct diagnoses and optimal use of break periods.

## Gameplay Description

### Game Structure
- **Start Screen**: Players are greeted with an overview of the game and a 'Start Game' button.
- **Main Game**: Players go through a series of patient interactions, each requiring a diagnosis based on presented symptoms.
- **Breaks**: At certain intervals, players can choose to rest or take on additional telemedicine cases for extra points.
- **End Game**: The game concludes after a set number of shifts or upon reaching an end condition, such as too many incorrect diagnoses.

### Game Flow
1. **Starting the Game**:
   - Players begin by clicking the 'Start Game' button.
   - A brief tutorial explains the game mechanics.

2. **Patient Diagnoses**:
   - Each patient case presents with different symptoms.
   - Players select a diagnosis from multiple choices.
   - Correct answers increase the player's score, while incorrect answers provide feedback and may penalize the player.

3. **Time Management**:
   - Players must manage in-game time, balancing between diagnosing patients and taking breaks.
   - Decisions made during breaks affect the player's energy and score.

4. **Scoring and Feedback**:
   - Points are awarded based on the accuracy of diagnoses and the efficiency of time management.
   - Feedback is provided at the end of each shift, summarizing the player's performance.

5. **Conclusion**:
   - The game ends with an overall performance review, including total score and areas for improvement.

## Game Mechanics
The game is designed to operate within a single web page, leveraging HTML, CSS, and JavaScript to create a seamless and dynamic user experience. The interface transitions between various states of gameplay—such as diagnosing patients, managing break times, and viewing game over screens—without the need to load new pages.

### Key Features:
- **Single-Page Application:** All components of the game are loaded once and displayed within a single page.
- **Dynamic Content Display:** Using CSS, particularly the `hidden` class, the game can show or hide elements without leaving the page, crucial for maintaining state and continuity in the gameplay.

## Technical Overview

### CSS and the `hidden` class
CSS plays a pivotal role in this project, especially in managing the visibility of elements on the page. The `.hidden` class is used extensively to control what the player sees at any point in time. This method is particularly effective in environments like Qualtrics, where the entire survey or simulation must run smoothly on a single page.

### Technologies Used
- **HTML5**: Structures the main content and layout of the game.
- **CSS3**: Provides styling to enhance the visual appeal and user interface.
- **JavaScript**: Implements the interactive elements and game mechanics.

### Main Components
- **index.html**: Hosts the structural layout of the game's interface.
- **style.css**: Defines all the CSS rules for the game, ensuring a consistent and engaging visual experience.
- **main.js**: Contains all the logic for game operation, including timers, game state management, and event handling.

### Detailed Breakdown of `main.js`
```javascript
## JavaScript Logic and Functionality

Below is a detailed breakdown of the key JavaScript functions used in the Hospital Simulator Game. These functions handle the game logic, manage the UI state, and ensure a smooth player experience:

```javascript
// Start the game by initializing game settings and displaying the first patient
function startGame() {
    resetScore();
    displayNewPatient();
    startTimer();
    hideElement('start-button');
    showElement('game-view');
}

// Display a new patient scenario by updating the UI with relevant information
function displayNewPatient() {
    const patientData = getPatientData();
    document.getElementById('patient-name').textContent = patientData.name;
    document.getElementById('patient-symptoms').textContent = patientData.symptoms;
    updateChoices(patientData.choices);
    hideElement('game-over');
    showElement('game-view');
}

// Start the main game timer and update the UI every second
function startTimer() {
    let startTime = Date.now();
    timerInterval = setInterval(function() {
        let elapsedTime = Date.now() - startTime;
        let minutes = Math.floor(elapsedTime / 60000);
        let seconds = ((elapsedTime % 60000) / 1000).toFixed(0);
        document.getElementById('timer').textContent = minutes + ':' + (seconds < 10 ? '0' : '') + seconds;
    }, 1000);
}

// Handle player's choice and decide the next step based on correctness
function handleChoice(isCorrect) {
    if (isCorrect) {
        increaseScore();
        displayNextPatient();
    } else {
        showFeedback('Incorrect. Try again!');
    }
}

// Increase the player's score for a correct diagnosis
function increaseScore() {
    score += 1;
    document.getElementById('score').textContent = 'Score: ' + score;
}

// Show or hide elements by adding/removing the 'hidden' class
function showElement(elementId) {
    document.getElementById(elementId).classList.remove('hidden');
}

function hideElement(elementId) {
    document.getElementById(elementId).classList.add('hidden');
}

// Stop the game timer and clean up resources
function stopGame() {
    clearInterval(timerInterval);
    showElement('game-over');
    hideElement('game-view');
}




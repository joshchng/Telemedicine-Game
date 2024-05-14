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
1. **Starting the Game/Introduction**:
   - Here players are also introduced to the common symptoms and diagnoses they may see.

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

## Game Mechanics
The game is designed to operate within a Qualtrics environment, leveraging HTML, CSS, and JavaScript to create a seamless and dynamic user experience. The interface transitions between various states of gameplay—such as diagnosing patients, managing break times, and viewing game over screens—without the need to load new pages.

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
  
### Future Directions
- **Fix Game Loop:** Working on resolving the game loop termination in the Qualtrics environment to ensure smooth gameplay and proper session endings.
- **JSON Loading:** Plans are underway to enhance the game's flexibility and scalability by allowing it to run based on a JSON file that describes various patient scenarios. This will facilitate easier updates and expansions of scenario data without altering the core game code.
- **Expand Scenarios:** We aim to enrich the gameplay experience by introducing more complex patient cases featuring multiple valid outcomes, thereby increasing the depth and educational value of the game.

## Game Logic Overview

Below is a simplified breakdown of the JavaScript functions used in the Hospital Simulator Game to manage game flow, timers, and player interactions:

```javascript
// Add onload function to set up the game when the page loads
Qualtrics.SurveyEngine.addOnload(function() {
    // Disable the default Qualtrics "Next" button to control flow manually
    this.disableNextButton();

    // Initialize game state variables
    let score = 0;  // Tracks the player's score
    let timerInterval;  // Controls the main game timer
    let breakTimerInterval;  // Manages break timers
    let telemedicineCount = 0;  // Tracks the number of telemedicine sessions handled

    // Define function to start a break timer
    function startBreakTimer(duration, callback) {
        let timer = duration;
        breakTimerInterval = setInterval(function () {
            // Calculate minutes and seconds from timer
            let minutes = parseInt(timer / 60, 10);
            let seconds = parseInt(timer % 60, 10);

            // Format and display the break timer
            document.getElementById('break-timer').textContent = "Break: " + formatTime(minutes) + ":" + formatTime(seconds);

            // Stop the timer and execute callback when time runs out
            if (--timer < 0) {
                clearInterval(breakTimerInterval);
                callback();
            }
        }, 1000);
    }

    // Define function to stop the break timer
    function stopBreakTimer() {
        clearInterval(breakTimerInterval);
        document.getElementById('break-timer').textContent = ''; // Clear break timer display
    }

    // Define function to start the main timer
    function startTimer() {
        let startTime = Date.now();
        timerInterval = setInterval(function() {
            // Calculate elapsed time and update display
            let elapsedTime = Date.now() - startTime;
            let minutes = Math.floor(elapsedTime / 60000);
            let seconds = Math.floor((elapsedTime % 60000) / 1000);
            document.getElementById('timer').textContent = 'Time: ' + formatTime(minutes) + ':' + formatTime(seconds);
        }, 1000);
    }

    // Define function to stop the main timer
    function stopTimer() {
        clearInterval(timerInterval);
    }

    // Define the game state object to manage scenes and transitions
    let gameState = {
        currentScene: 'intro',  // Start with the introduction scene
        scenes: {
            intro: {
                title: "Introduction",
                story: "Good morning. Let's begin your shift.",
                chart: `<table>...</table>`,  // Display a table of diseases and symptoms
                choices: [
                    { text: "Yes, I'm ready!", next: 'patient1' }
                ]
            },
            patient1: {
                title: "Patient 1",
                // Additional patient scenarios and logic here...
            }
            // Define other scenes and logic as needed...
        },

        // Define function to display a specific scene
        displayScene: function(sceneKey) {
            let scene = this.scenes[sceneKey];
            // Update UI components based on the current scene
            document.getElementById('scene-title').textContent = scene.title;
            document.getElementById('scene-story').textContent = scene.story;
            document.getElementById('disease-chart').innerHTML = scene.chart || '';

            let choicesContainer = document.getElementById('choices');
            choicesContainer.innerHTML = ''; // Clear previous choices
            if(scene.onEnter) scene.onEnter(); // Execute additional logic when entering the scene

            // Create buttons for each choice in the scene
            scene.choices.forEach(choice => {
                let btn = document.createElement('button');
                btn.textContent = choice.text;
                btn.onclick = () => {
                    this.displayScene(choice.next); // Handle choice selection
                };
                choicesContainer.appendChild(btn);
            });
        },

        // Define function to show the main game view
        showGameView: function() {
            document.getElementById('game-view').classList.remove('hidden');
            document.getElementById('start-button').classList.add('hidden');
        }
    };

    // Start the game when the 'Start Game' button is clicked
    document.getElementById('start-button').addEventListener('click', function() {
        console.log('Starting game...');
        score = 0; // Reset score
        gameState.displayScene('intro'); // Display the intro scene
        startTimer(); // Start the main game timer
    });

    // Additional helper functions...
});

// Helper function to format time values as two digits
function formatTime(number) {
    return number < 10 ? '0' + number : number;
}





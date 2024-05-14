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





# MEMORY GAME 

This project is a memory game created using Vue.js. The user completes the game by trying to match colored cards. It has game start, pause and reset features.

https://github.com/aysunurterzi/Memory_Game_Vue/assets/80470813/5c666e8c-1472-425a-ab51-004525857d78

## Features

- **Start/Reset Button**: Starts or resets the game. It appears green when the game starts and red when it resets.
- **Pause/Resume Button**: Pauses or continues the game. It appears orange when paused and yellow when resuming.
- **Counter**: Shows game time in seconds.
- **Win Screen**: When all cards are matched, a congratulations message is displayed showing the user's time.
- **Game Logic**: Cards are shuffled randomly and remain open when both cards are matched.

## Setup

To run the project, follow these steps:

1. Clone this repo:
     ```bash
     git clone https://github.com/username/memory-game.git
     ```
2. Go to the project directory:
     ```bash
     cd memory-game
     ```
3. Install the required packages:
     ```bash
     npm install
     ```
4. Start the application:
     ```bash
     npm run serve
     ```

## Use

- **Start**: Starts the game and shuffles the cards.
- **Pause**: Pauses the game and the timer stops.
- **Continue**: Continues the paused game.
- **Reset**: Reset the game and reshuffle the cards.
- **Card Selection**: Try to match the cards by clicking on them. Matching cards remain face up, unmatched ones turn grey.

## File Structure

- `src/components/MemoryCard.vue`: Card component.
- `src/components/GameBoard.vue`: Game board component.
- `src/App.vue`: Main application component.
- `src/main.js`: Application startup file.

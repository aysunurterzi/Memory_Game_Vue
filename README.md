# 🧠 Memory Game - Vue.js

<div align="center">
  <h3>🎮 A Beautiful Memory Card Matching Game Built with Vue.js</h3>
  <p>Test your memory skills by matching pairs of colorful animal cards!</p>
  
  ![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=for-the-badge&logo=vue.js&logoColor=white)
  ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
  ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
  ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
</div>

---

## 📖 About The Project

This is an interactive memory game where players flip cards to find matching pairs of cute animal images. The game features a clean, modern interface with smooth animations and intuitive controls. Perfect for players of all ages who want to exercise their memory skills while having fun!

### 🎥 Demo

<div align="center">
  <p><strong>🎮 Watch the Memory Game in action!</strong></p>
  
 

https://github.com/user-attachments/assets/12647f6d-c422-44b7-bf7a-bfe17a792db0


  
  <p><em>🎯 See how easy it is to match the cute animal pairs!</em></p>
</div>

---

## ✨ Features

### 🎮 Game Controls
- **🚀 Start/Reset Button**: 
  - 🟢 **Green**: Click to start a new game
  - 🔴 **Red**: Click to reset current game
- **⏸️ Pause/Resume Button**: 
  - 🟠 **Orange**: Game is paused
  - 🟡 **Yellow**: Click to resume
- **⏱️ Timer**: Real-time game duration tracking
- **🏆 Victory Screen**: Celebratory message with your completion time

### 🎯 Game Mechanics
- **🔀 Smart Shuffling**: Cards are randomly shuffled each game
- **🧩 Memory Challenge**: Find matching pairs by flipping two cards
- **💡 Visual Feedback**: 
  - Matched cards stay face-up
  - Unmatched cards flip back after a brief moment
- **🎊 Win Condition**: Match all pairs to complete the game

### 🎨 Visual Design
- Beautiful animal-themed card designs
- Smooth card flip animations
- Responsive layout for all screen sizes
- Modern, clean user interface

---

## 🛠️ Technology Stack

- **Frontend Framework**: Vue.js 3
- **Language**: JavaScript (ES6+)
- **Styling**: CSS3 with custom animations
- **Build Tool**: Vue CLI
- **Package Manager**: npm

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed:
- **Node.js** (version 14 or higher)
- **npm** (comes with Node.js)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/aysunurterzi/Memory_Game_Vue.git
   ```

2. **Navigate to the project directory**
   ```bash
   cd Memory_Game_Vue
   ```

3. **Install dependencies**
   ```bash
   npm install
   ```

4. **Start the development server**
   ```bash
   npm run serve
   ```

5. **Open your browser**
   
   The game will be available at `http://localhost:8080`

### Build for Production

To create a production build:
```bash
npm run build
```

---

## 🎮 How to Play

1. **🎯 Objective**: Match all pairs of animal cards
2. **🖱️ Click**: Tap any card to flip it over
3. **🧠 Remember**: Try to remember the positions of different animals
4. **🎯 Match**: Click another card to find its pair
5. **✅ Success**: Matched pairs stay face-up
6. **❌ Miss**: Unmatched cards flip back over
7. **🏆 Win**: Match all pairs to complete the game!

---

## 📁 Project Structure

```
Memory_Game_Vue/
├── 📁 public/
│   ├── 🌐 index.html          # Main HTML template
│   └── 🖼️ favicon.ico         # App icon
├── 📁 src/
│   ├── 📁 assets/
│   │   └── 📁 img/            # Animal card images
│   │       ├── 🐱 cat.png
│   │       ├── 🐊 crocodile.png
│   │       ├── 🐕 dog.png
│   │       ├── 🦆 duck.png
│   │       ├── 🐘 elephant.png
│   │       ├── 🦒 giraffe.png
│   │       ├── 🦁 lion.png
│   │       └── 🐰 rabbit.png
│   ├── 📁 components/
│   │   ├── 🎮 GameBoard.vue   # Main game logic & board
│   │   └── 🃏 MemoryCard.vue  # Individual card component
│   ├── 📱 App.vue             # Root component
│   └── ⚡ main.js             # Application entry point
├── ⚙️ package.json            # Dependencies & scripts
├── 🔧 vue.config.js           # Vue configuration
└── 📖 README.md              # Project documentation
```

### Component Details

- **`App.vue`**: Root component that orchestrates the entire application
- **`GameBoard.vue`**: Contains game logic, timer, controls, and card grid layout
- **`MemoryCard.vue`**: Reusable card component with flip animations and click handling

---

## 🎨 Game Assets

The game features beautiful hand-selected animal images:
- 🦁 Lion
- 🐘 Elephant  
- 🐱 Cat
- 🐕 Dog
- 🦆 Duck
- 🐰 Rabbit
- 🐊 Crocodile
- 🦒 Giraffe

---

## 🤝 Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

---

## 👩‍💻 Author

**Aysunur Terzi**
- GitHub: [@aysunurterzi](https://github.com/aysunurterzi)

---

## 🙏 Acknowledgments

- Vue.js community for the amazing framework
- All the animal image contributors
- Everyone who has contributed to making this project better

---

<div align="center">
  <p>⭐ Star this repo if you found it helpful!</p>
  <p>🎮 Enjoy playing the Memory Game!</p>
</div>

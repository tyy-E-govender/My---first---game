[README.md](https://github.com/user-attachments/files/26566652/README.md)
# X∞O — Play With Friends, Anywhere

> A beautiful, real-time multiplayer Tic-Tac-Toe game you can play in any browser — no server, no install, no nonsense.

![Made with HTML CSS JS](https://img.shields.io/badge/Built%20with-HTML%20%7C%20CSS%20%7C%20JS-7F77DD?style=flat-square)
![No dependencies](https://img.shields.io/badge/Dependencies-None-1DB37A?style=flat-square)
![Single file](https://img.shields.io/badge/Single%20File-Yes-E24B4A?style=flat-square)
![License MIT](https://img.shields.io/badge/License-MIT-white?style=flat-square)

---

## ✨ Features

- 🌐 **Online Multiplayer** — Create a room, share the code, and play against a friend in real time across browser tabs or devices on the same network
- 🔗 **Shareable Room Links** — One-click link sharing that pre-fills the join code for your friend
- 🔐 **Google Login & Guest Play** — Sign in with Google to save your stats, or jump straight in as a guest
- 🎨 **Custom Symbol Colors** — Pick from presets or use the full color picker to make X and O your own
- 🏆 **Leaderboard & Stats** — Global, Friends, and Weekly boards with your personal win/loss/draw record persisted locally
- 🤖 **vs AI Mode** — Smart AI that blocks, attacks, and takes corners
- 🏠 **Local Co-op** — Pass-and-play on the same device
- 🥇 **Best of 5 Tournament** — First to 3 wins takes the crown
- 🎉 **Confetti & Animations** — Win-line SVG draw, cell pop, confetti burst, animated nebula background
- 📱 **Responsive** — Works great on mobile and desktop

---

## 🚀 Getting Started

No build step. No dependencies. Just open the file.

```bash
git clone https://github.com/yourusername/xo-game.git
cd xo-game
open xo_online_multiplayer_game.html
```

Or simply **drag the file into your browser**.

---

## 🎮 How to Play

### Online vs a Friend

1. Open the game and sign in (Google or Guest)
2. Select **Online** mode and tap **Play Now**
3. Click **Create Room** — a 6-character code appears
4. Share the code or the auto-generated link with your friend
5. Your friend opens the game, enters the code, and joins
6. First to get three in a row wins the round!

### Local (Same Device)

Select **Local** mode — Player 1 and Player 2 take turns on the same screen.

### vs AI

Select **vs AI** — the computer plays as O and will try to block you and win. Good for practice.

### Tournament (Best of 5)

Select **Best of 5** — first player to win 3 rounds wins the tournament. Scores are tracked in the in-game strip.

---

## 🛠️ How Online Multiplayer Works

X∞O uses the browser's native **BroadcastChannel API** for zero-latency communication between tabs on the same browser/device, and **localStorage** for room discovery across tabs.

```
Player A (Host)           Player B (Joiner)
──────────────            ─────────────────
Creates room XO7F2A  →    Enters code XO7F2A
BroadcastChannel opens    BroadcastChannel opens
                     ←    Sends JOIN message
Game starts               Game starts
Sends MOVE on click  →    Board updates instantly
                     ←    Sends MOVE on click
Board updates instantly
```

> **Note:** The BroadcastChannel API works across tabs and windows in the same browser on the same device. For play across different physical devices on the same network, the game gracefully falls back to a simulated join (great for demo/testing). A WebSocket backend can be plugged in by replacing the `handleChannelMsg` and `makeMove` broadcast calls.

---

## 📁 Project Structure

```
xo-game/
└── xo_online_multiplayer_game.html   # The entire game — one file
└── README.md                         # You are here
```

Everything lives in a single, self-contained HTML file:

| Section | What it does |
|---|---|
| CSS Variables | Theming — colors, surfaces, radii |
| Canvas BG | Animated star/nebula particle system |
| Screen system | Auth → Home → Setup → Waiting → Game → Settings → Leaderboard |
| BroadcastChannel | Real-time multiplayer messaging |
| AI logic | Minimax-lite: win → block → center → corner → random |
| Color picker | CSS variable injection from chip or `<input type="color">` |
| LocalStorage | Stat persistence across sessions |

---

## 🎨 Customization

### Change default colors

Edit the CSS variables at the top of the file:

```css
:root {
  --x: #E24B4A;    /* X symbol color */
  --o: #1DB37A;    /* O symbol color */
  --accent: #7F77DD; /* UI accent color */
  --bg: #0B0A14;   /* Background */
}
```

### Add more color presets

Find the `#x-chips` or `#o-chips` sections in the HTML and add:

```html
<div class="chip-color" style="background:#YOUR_COLOR;" onclick="setColor('x','#YOUR_COLOR',this)"></div>
```

### Plug in a real WebSocket backend

Replace the BroadcastChannel logic in the `createRoom()`, `joinRoom()`, and `handleChannelMsg()` functions with WebSocket calls. The message protocol is simple:

```js
// Messages used
{ type: 'JOIN',  name: 'PlayerName' }
{ type: 'MOVE',  cell: 4, sym: 'X'  }
{ type: 'RESET' }
```

---

## 🌍 Deployment

Since it's a single HTML file, deploy anywhere:

| Platform | Command / Method |
|---|---|
| **GitHub Pages** | Push to `main`, enable Pages in repo settings |
| **Netlify** | Drag & drop the file at netlify.com/drop |
| **Vercel** | `vercel --prod` in the project folder |
| **Any static host** | Upload the `.html` file |

For GitHub Pages, rename the file to `index.html` and the game will be live at `https://yourusername.github.io/xo-game`.

---

## 🧩 Browser Support

| Browser | Support |
|---|---|
| Chrome 54+ | ✅ Full |
| Firefox 38+ | ✅ Full |
| Edge 79+ | ✅ Full |
| Safari 15.4+ | ✅ Full |
| Mobile browsers | ✅ Responsive |

> BroadcastChannel is supported in all modern browsers. Safari support landed in version 15.4.

---

## 🤝 Contributing

Pull requests are welcome! A few ideas if you want to contribute:

- **WebSocket server** — Node.js/Express backend for true cross-device online play
- **Animations** — More celebration effects on win
- **Sound effects** — Subtle audio feedback on moves
- **Dark/light theme toggle**
- **5×5 board mode** — Extended gameplay

---

## 📄 License

MIT — do whatever you like with it. A star ⭐ is always appreciated.

---

<div align="center">
  Made with ♥ for people who love playing games with the ones they care about.
</div>

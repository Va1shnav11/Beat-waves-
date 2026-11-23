# 🎵 Beat Waves

**A retro-vinyl music playlist manager built on a doubly linked list.**

Beat Waves is a single-file web app created as a Data Structures project. It looks and feels like a music player, but under the hood every playlist is a hand-written **doubly linked list**. A built-in **Inspect** tab shows the list's nodes and pointers live, so you can watch the data structure change as you use the app.

---

## ✨ Features

- **Playlist management**: create, rename, switch between and delete multiple playlists
- **Add songs** at the start, at the end, or at any chosen position
- **Upload real audio files** (stored in your browser) or add a song with a **generated tune**
- **Reorder** songs (move up / move down) and **remove** them, with an **Undo** option
- **Playback controls**: play/pause, next, previous, seek bar, shuffle, repeat (off / all / one)
- **Search** songs by title or artist
- **Vinyl player UI** with a spinning record, tonearm animation and equalizer bars
- **Inspect tab**: a live visualisation of HEAD, TAIL, each node's `prev` / `next` links, and a log of recent operations with their time complexity
- **Responsive layout**: phone (bottom tabs + mini player), tablet and desktop (three-column layout)
- **Persistent data**: playlists are saved in `localStorage`, audio files in `IndexedDB`
- Respects `prefers-reduced-motion`

---

## 🧠 Data Structure: Doubly Linked List

Each song is stored in a `Node` that holds links to the previous and next songs.

```js
class Node {
  constructor(song) { this.song = song; this.prev = null; this.next = null; }
}
```

The `Playlist` class maintains `head`, `tail` and `size`, and provides:

| Method | Description | Time Complexity |
|---|---|---|
| `addFirst(song)` | Insert at the start | O(1) |
| `addLast(song)` | Insert at the end (via `tail`) | O(1) |
| `insertAt(i, song)` | Insert at position `i` | O(n) |
| `nodeAt(i)` | Get the node at index `i` (walks from the nearer end) | O(n) |
| `removeNode(node)` | Unlink a node (given a reference to it) | O(1) |
| `indexOf(node)` | Find a node's position | O(n) |
| `toArray()` | Traverse head → tail | O(n) |

**Why a doubly linked list?**
- The `prev` pointer makes the **Previous song** button a simple O(1) step.
- Removal needs no walk from the head once the node is known.
- `tail` gives O(1) appends, and `nodeAt` can start from whichever end is closer.
- Moving a song is implemented as `removeNode` followed by `insertAt`.

---

## 🚀 Getting Started

No build step, no dependencies, no installation.

1. Clone the repository
   ```bash
   git clone https://github.com/<your-username>/beat-waves.git
   cd beat-waves
   ```
2. Open `index.html` in any modern browser (double-click it, or serve it locally):
   ```bash
   python -m http.server 8000
   # then visit http://localhost:8000
   ```

> **Note:** Fonts (Fraunces, Karla, Courier Prime) load from Google Fonts, so an internet connection is needed for the intended look. The app still works offline with fallback fonts.

---

## 🕹️ How to Use

1. **Songs tab**: browse the current playlist, search, and tap a song to play it. Tap **⋯** on a song to move or remove it. Tap **+** to add songs.
2. **Playing tab**: control playback, seek, shuffle and repeat. On desktop the player is always visible on the right.
3. **Playlists tab**: create a new playlist, open one, rename it or delete it (⋯ menu).
4. **Inspect tab**: watch the linked list update after every add, move or remove.

**Adding a song**
- *Real track*: choose one or more audio files. If you pick a single file you can override its title, artist and length.
- *Generated tune*: leave the file empty, then enter a title, artist and length (`m:ss`). A short looping melody is synthesised with the Web Audio API, unique to each title.

The **Demo speed** chip (1× / 10× / 30×) speeds up generated tunes only, which is handy for testing "next song" and end-of-playlist behaviour.

---

## 🛠️ Tech Stack

- **HTML5 / CSS3**: custom properties, grid, flexbox, container queries, CSS animations
- **Vanilla JavaScript (ES6+)**: no frameworks or libraries
- **Web Audio API**: generated tunes
- **HTMLAudioElement**: real audio file playback
- **localStorage + IndexedDB**: persistence

---

## 📁 Project Structure

```
beat-waves/
├── index.html   # entire app: markup, styles and scripts
└── README.md
```

Inside the script, the code is organised as: linked list classes → state → helpers → storage → sound → playback → rendering → UI event handlers.

---

## 🔮 Possible Improvements

- Drag-and-drop reordering
- Move or copy songs between playlists
- Import / export playlists as JSON
- Album art and metadata (ID3) reading
- Queue view and volume control

---

## 👥 Team

| Name | USN | Role |
|---|---|---|
| Siri Patil | NB25ISE229 | Doubly linked list implementation (`Node`, `Playlist` class) |
| Vaishnavi C | NB25ISE258 | UI / Design (vinyl player, animations, responsive layout) |
| Varsha N | NB25ISE259 | Audio playback and storage (Web Audio API, `localStorage`, `IndexedDB`) |
| Yashika D Gowda | NB25ISE275 | Inspect tab, testing and documentation |

*Data Structures Project, Information Science & Engineering, 2026*

---

## 📄 License

This project is for educational purposes.

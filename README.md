# 🎵 Liquid Dream Music Player 🎧

**A premium, glassmorphism-style web music player with a realistic physical turntable experience.**

🌐 **Live Website:**  
👉 https://sahibdeepme.github.io/Music-Player/ 👈

---

## 📖 About

<img src="https://i.postimg.cc/FzKW51y2/Screenshot-2025-12-21-193737.png"
     align="right"
     width="260"
     alt="Liquid Dream Player Preview" />

Liquid Dream is a modern **web-based music player** designed for users who love the **feel of vintage vinyl** combined with a **clean, futuristic UI**.

The player does more than just play audio. It visually and logically simulates:
- a spinning vinyl record  
- a mechanical tonearm  
- smooth, responsive playback behavior  

Music can be loaded from a **remote GitHub repository** or directly from the **user’s local folder**, making it powerful yet privacy-friendly.

<br clear="right"/>

---

## 🖼️ Interface Preview

<img src="https://i.postimg.cc/G2wL38qy/Screenshot-2025-12-21-204358.png"
     width="100%"
     alt="Liquid Dream Interface Preview" />

---

## ✨ Features

- 💿 **Realistic Vinyl Animation** – Smooth CSS-based rotation
- 🕹️ **Mechanical Tonearm Logic** – Moves on play / pause
- ☁️ **GitHub Music Library** – Remote songs loaded via API
- 📂 **Local Folder Support** – Play music from your own device
- 💾 **Persistent Storage** – Remembers your folder permission
- 🎧 **Pure Web App** – No backend, no tracking

---

## 🧠 Music Player Database Structure

Liquid Dream uses a **three-layer data system** to balance performance, privacy, and persistence.

---

### 🌐 1️⃣ Remote Data Source (Predefined Library)

This is the **default music library** available to all users.

- **Service:** GitHub REST API (v3)
- **Repository Owner:** `SahibdeepMe`
- **Repository Name:** `Music-Player`
- **Folder Path:** `/Songs`
- **Formats Supported:** `.mp3`, `.wav`, `.ogg`, `.m4a`

**Logic:**
- The app performs a `GET` request to the GitHub API
- The returned JSON is parsed
- `download_url` → used as the audio source
- `name` → cleaned using RegEx to generate song titles

📌 This library is **read-only** and works as the global default playlist.

---

### 💾 2️⃣ Local Browser Storage (Persistent State)

To remember the user’s selected local music folder, the app uses **IndexedDB**.

- **Database Type:** IndexedDB (Browser-based NoSQL)
- **Library Used:** `idb-keyval`
- **Key:** `songs-folder-handle`
- **Value:** `FileSystemDirectoryHandle` object

**Purpose:**
- Stores permission to the user’s local music folder
- On page reload, the app automatically re-requests access
- Safer and more powerful than `localStorage`

🔐 Your music **never leaves your device**.

---

### ⚡ 3️⃣ In-Memory State (Session Data)

While the app is running, it maintains a temporary playlist state in memory.

**Main Variables:**
```js
playlist[]            // Master list of songs
filteredPlaylist[]    // Search results
currentLoadedIndex    // Currently playing song index

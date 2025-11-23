
# 🎮 Multiplayer Phaser Game with Voice Chat

This project is a **real-time multiplayer Phaser 3 game** built using:

* **Phaser 3** – for game scenes, animations, physics
* **React** – for mounting the game inside a component
* **Socket.io** – for real-time multiplayer sync
* **WebRTC + freeice** – for *proximity-based voice chat*
* **Express Node.js Server** – managing rooms, players, and signaling

Players can:

✔ Create a room
✔ Join an existing room
✔ Move around in the world
✔ See other players move in real time
✔ Talk using voice chat when they are nearby
✔ Leave room and return to the lobby

---

# 🚀 Features

### 🎯 **1. Room System**

Players can **create** or **join** rooms with:

* Room Name
* Username
* Password

Server validates and manages room data.
(Handled in `createRoom` & `joinRoom` events )

---

### 🧍‍♂️🧍‍♀️ **2. Real-Time Multiplayer Movement**

Client sends:

```
socket.emit("move", { x, y, direction, isMoving })
```

Server broadcasts to all other players in the same room.
(Implemented in `playerMoved` listening logic in Scene2) 

---

### 🎤 **3. Proximity Voice Chat**

Players can talk through WebRTC:

* Voice connects only when players are **within 200px**
* Auto-mutes when far away
* Manual mute button available
  (Voice logic via WebRTC peer connections) 

---

### 📺 **4. Beautiful Waiting Room UI**

Includes:

* Create Room tab
* Join Room tab
* Animated cartoon characters reacting to text field focus
  (Rendered using Phaser DOM elements) 

---

### 🕹 **5. Smooth Player Animation**

Walking animations for:

* Up
* Down
* Left
* Right
  (Loaded from sprite sheets) 

---

### ↩️ **6. Leave Room Support**

Players can click "Leave Room" to:

* Stop audio tracks
* Close WebRTC connections
* Remove player on server
  (Handled in the `leaveRoom` function) 

---

# 📦 Project Structure

```
/client
   └── Game.jsx (Phaser + React game code)

/server
   └── server.js (Express + Socket.io servidor)
```

---

# ⚙️ How to Run the Project

## 1️⃣ **Install Dependencies**

### Client

```
cd client
npm install
```

### Server

```
cd server
npm install
```

---

# ▶️ 2️⃣ **Start the Server**

```
cd server
node server.js
```

Server runs on:
👉 **[http://localhost:3000](http://localhost:3000)**

---

# 🎮 3️⃣ **Run the Client React App**

```
cd client
npm run dev
```

Client runs on something like:
👉 **[http://localhost:5173](http://localhost:5173)**

---

# 🌐 **How the System Works (High-Level)**

### **1. Player enters the waiting room**

UI rendered inside Phaser (DOM element).

### **2. Create or Join Room**

Client sends to server:

```
socket.emit("createRoom" | "joinRoom", {...})
```

### **3. Game Scene Loads**

Phaser Scene2 starts:

* Loads background
* Creates player sprite
* Connects with room
* Sends `playerReady`

### **4. Real-time Sync**

Server sends:

* New players
* Movements
* Player removals

### **5. WebRTC Voice Chat**

* When a remote player enters 200px range → unmute
* When far → auto mute
* Uses freeice for STUN/TURN

### **6. Leave Room**

Everything resets and returns to waiting room.

---

# 🔧 Technologies Used

| Tech                       | Purpose               |
| -------------------------- | --------------------- |
| **Phaser 3**               | Rendering & physics   |
| **React**                  | Hosting game in SPA   |
| **Socket.io**              | Real-time multiplayer |
| **Express**                | Node backend          |
| **WebRTC**                 | Voice chat            |
| **freeice**                | ICE server generation |
| **DOM Elements in Phaser** | Custom UI             |

---

# 📚 API Events (Socket.io)

### Client → Server

* `createRoom`
* `joinRoom`
* `playerReady`
* `move`
* `voiceOffer`
* `voiceAnswer`
* `voiceCandidate`
* `leaveRoom`

### Server → Client

* `roomError`
* `roomCreated`
* `roomJoined`
* `currentPlayers`
* `newPlayer`
* `playerMoved`
* `removePlayer`
* Voice signaling events

---

# 🧪 Future Improvements (Optional)

* Add mini-games on tables
* In-game chat
* 3D isometric view
* Lobby chat
* Player avatars

---
<img width="605" height="604" alt="image" src="https://github.com/user-attachments/assets/237cc56e-e1ae-48a0-801c-18dc9108ed45" />

<img width="589" height="554" alt="image" src="https://github.com/user-attachments/assets/cf3c6245-7529-4682-add9-572f9db37d3d" />

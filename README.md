

````markdown
# Live Website Viewer Counter (Firebase + JS)

This project lets you display the **real-time number of concurrent visitors** on your website using Firebase Realtime Database.  
It’s a lightweight drop-in script that you can serve from GitHub or a CDN.

---

## 🚀 Features
- **Real-time** concurrent user count (updates instantly when people join/leave)
- **Per-page tracking** — each page has its own count
- **Automatic cleanup** — disconnects are handled and stale entries removed
- Can be **served via CDN** from GitHub, jsDelivr, or Statically

---

## 📦 1. Setup Firebase
1. Go to [Firebase Console](https://console.firebase.google.com/), create a project.
2. Add a **Realtime Database** (in test mode for quick start).
3. Copy your Firebase config from **Project Settings → General → Your apps → Firebase SDK snippet**.
4. Replace the `firebaseConfig` in `livecount.js` with your values.

---

## 📄 2. Host `livecount.js`
You can host this file in your GitHub repository and then use:

**Direct GitHub Raw (not recommended for heavy traffic)**
```html
<script src="https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/livecount.js"></script>
````

**Using jsDelivr (recommended)**

```html
<script src="https://cdn.jsdelivr.net/gh/forzayt/LiveCountCDN/livecount.js"></script>
```



---

## 🖥 3. Include in Your Website

Example HTML:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Live Viewers</title>
  <!-- Firebase SDKs -->
  <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>

  <!-- Your livecount.js script -->
  <script src="https://cdn.jsdelivr.net/gh/forzayt/LiveCountCDN/livecount.js"></script>
</head>
<body>


       <!-- use id ="livecount" for UI -->
        
  <h1>Live Visitors: <span id="livecount">0</span></h1>



  
</body>
</html>
```

---

## 🔑 4. How It Works

* Each visitor is assigned a unique ID and added to a `viewers/<page>` node in Firebase.
* When they leave (tab close, refresh), Firebase `onDisconnect()` removes them.
* The script listens for changes and updates the `<span id="livecount">` value in real-time.
* `id="room"` will show the current page's path as the "room name".

---

## ⚠ Notes

* Make sure your Firebase **Realtime Database rules** allow read/write for testing:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

* For production, add authentication or restrict writes to avoid abuse.
* `id="livecount"` **must exist in your HTML** — the script updates this element.
* `id="room"` is optional — only needed if you want to display the page/room name.

---

## 📷 Example Output

**On your site:**

```
Live Visitors: 5
Room: /index.html
```

Updates instantly when new visitors arrive or leave.

---

```


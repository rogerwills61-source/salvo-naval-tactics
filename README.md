# SALVO! — 3D Comic Naval Tactics

**SALVO!** is a fast-paced, 3D tactical naval artillery game styled like a 1970s/80s living war comic. Command a custom five-vessel cast-pewter task force across twin 10×10 tactical sea charts, outmaneuver **Commodore AI** in Solo mode, or challenge a friend across devices using a 5-character radio room code or direct invite link.

### Key Features

* **Tactical Kill-Streak Salvo Rules:** Alternate salvos across separate defensive (**YOUR FLEET**) and offensive (**ENEMY WATERS**) 10×10 grids. Sinking the final square of any enemy warship immediately awards a **Bonus Shot**, letting sharp-eyed commanders chain consecutive kills.
* **Sculpted 3D Pewter Miniature Fleet:** Five distinct warship classes—**Dreadnought** (5), **Ironclad** (4), **Frigate** (3), **Corvette** (3), and **Gunboat** (2)—rendered with metallic bevels, enamel class trim, ink outlines, parabolic artillery shells, continuous firework sinking streams, and a 360° Kill-Cam orbit.
* **Solo vs. Commodore AI with Auto-Save:** Battle a parity-hunting, target-tracking AI opponent whose match progress automatically saves in your browser so you can close the app and resume mid-battle anytime.
* **Cross-Device 2-Player Multiplayer:** Host a private room with an instant 5-character room code or one-click invite link (`?room=XXXXX`) with strict Fog-of-War privacy until vessels are sunk.
* **Responsive Desktop & Mobile Controls:** Side-by-side dual-sea camera on desktop/landscape and an overhead tactical chart with automatic 3D firing cutaways on portrait phones—plus one-tap install as a standalone app.

---

## Installation Instructions (By Platform)

Once hosted over HTTPS (such as **GitHub Pages**), **SALVO!** can be installed directly onto your device as a standalone app. The in-app **`📲 INSTALL SALVO! APP`** button automatically hides itself once installed.

### Android (Chrome, Edge, Brave, Samsung Internet)
1. Open the hosted game URL in your mobile browser.
2. Tap **`📲 INSTALL SALVO! APP`** in the main menu (or open the browser's **`⋮` menu** and tap **Install app** / **Add to Home screen**).
3. Confirm **Install**—**SALVO!** will appear on your Home Screen and launch full-screen without browser bars.

### iPhone & iPad (iOS / iPadOS Safari)
1. Open the hosted game URL in **Safari**.
2. Tap **`📲 INSTALL SALVO! APP`** in the main menu to view the quick prompt, or tap Safari's **Share** button (the square with an upward arrow).
3. Scroll down and select **Add to Home Screen**, then tap **Add**.
4. Launch **SALVO!** from your Home Screen icon for full-screen standalone play.

### Windows & macOS Desktop (Chrome, Edge, Brave)
1. Open the hosted game URL in Chrome, Edge, or Brave.
2. Click **`📲 INSTALL SALVO! APP`** in the main menu (or click the **Install** icon in the right side of the browser address bar).
3. Click **Install** to add **SALVO!** to your Desktop, Start Menu, or macOS Applications / Dock.

### Local Offline Play (No Web Server Required)
* Download `index.html` and open it directly in any modern web browser on Windows, macOS, or Linux to play Solo vs. Commodore AI immediately.

---

## Deploying to GitHub Pages

1. Create a new public repository on GitHub (for example, `salvo-naval-tactics`).
2. Upload **`index.html`** and **`README.md`** to the root of the repository (`main` branch).
3. Go to **Settings → Pages**, set **Source** to **Deploy from a branch**, select **`main`** and **`/ (root)`**, and click **Save**.
4. Open your published `https://<username>.github.io/<repo-name>/` URL on any phone, tablet, or computer.

---

## Technical Architecture

* **Zero-Build Single-File Runtime (`index.html`):** Self-contained HTML5, CSS3, and ES6+ JavaScript requiring no bundler, build step, or backend server.
* **3D Rendering & Physics (`Three.js r128`):**
  * Custom procedural studio environment reflection map (`createPewterEnvMap`) with `ACESFilmicToneMapping` and crisp `EdgesGeometry` comic ink lines.
  * Wall-clock linear-time parabolic shell ballistics synchronized to procedural Web Audio synthesis (`AudioContext` cannon boom, falling artillery whistle, splash, and multi-layered explosions).
  * Responsive portrait/landscape camera controller featuring sticky per-sea pinch-zoom/pan, full-extents 3D action cutaways, and shortest-angle spherical interpolation for the 360° Kill-Cam.
* **Progressive Web App (PWA) Layer (`pwaInstall`):**
  * Dynamically generates 192×192 and 512×512 PNG app icons on an offscreen `<canvas>`, injects a `Blob`-backed Web App Manifest (`display: "standalone"`), registers a network-first/cache-fallback Service Worker over HTTPS, and listens to `beforeinstallprompt`, `appinstalled`, and `display-mode: standalone` to hide the install button automatically once installed.
* **Cross-Device Multiplayer & Persistence:**
  * Uses **MQTT over Secure WebSockets (`wss://`)** (`broker.emqx.io` with automatic failover to `broker.hivemq.com`) and a `BroadcastChannel` fallback for local multi-tab testing, paired with `localStorage` (`salvo_ai_battle_v1`) for mid-match Solo AI save/resume.
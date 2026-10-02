# Wispr Fish 🐟🤫

> A voice-driven, sound-sensitive top-down stealth heist game built with plain JavaScript, HTML5 Canvas, and the Web Audio API. No external libraries, CDNs, or third-party APIs.

---

## 🎮 Hands-Free Voice Controls (No Keyboard Needed!)

You can play through the entire game **without touching a keyboard**, using only your **voice** and sound!

### 1. Voice Navigation & Learned Speed Pace
- **Voice Commands** (powered by native Web Speech recognition or HUD interactive buttons):
  - **&ldquo;Front&rdquo; / &ldquo;Forward&rdquo; / &ldquo;Go&rdquo;**: Move forward in the facing direction at the active pace.
  - **&ldquo;Back&rdquo; / &ldquo;Backward&rdquo; / &ldquo;Reverse&rdquo;**: Turn around 180° immediately and move away from guards or walls at the active pace.
  - **&ldquo;Fast&rdquo; / &ldquo;Sprint&rdquo; / &ldquo;Run&rdquo;**: Sets learned pace to **⚡ FAST** (3.6 px/frame). Fast pace stays active across subsequent &ldquo;Front&rdquo; or &ldquo;Back&rdquo; or turn commands until changed.
  - **&ldquo;Okay&rdquo; / &ldquo;Slow&rdquo; / &ldquo;Normal&rdquo;**: Sets pace back to **🐢 SLOW** (0.95 px/frame). This is the default stealth creep pace with muffled footsteps (noise capped to 28 px) and reduced spotted rate to slip safely past guards (&ldquo;police cars&rdquo;).
  - **&ldquo;Stop&rdquo; / &ldquo;Wait&rdquo; / &ldquo;Halt&rdquo;**: Immediately brings the thief to a full halt. The game also starts safely in STOP mode on level load so the thief never runs away automatically.
  - **&ldquo;Left&rdquo; / &ldquo;Right&rdquo;**: Turn 90° in that direction (debounced to avoid multiple rapid interim turns).
  - **&ldquo;Restart&rdquo;**: Instantly restart after being caught.
- **HUD Speed & Direction Pills**:
  - Click any of the interactive buttons in the HUD (`🐢 OKAY (SLOW)`, `⚡ FAST`, `▲ FRONT`, `▼ BACK`, `🛑 STOP`) for instant tactile control.
- **Acoustic Voice Throttle**:
  - Speaking adds dynamic sound waves and propulsion in real-time.
  - **Whispering** (&sim; -45 to -35 dB): Safe stealth voice.
  - **Normal Voice** (&sim; -30 to -18 dB): Standard voice level.
  - **Loud Voice / Shout** (&gt; -12 dB): Triggers a **Shout Dash** burst shockwave!
- **Tone & Pitch Steering**:
  - **Low Pitch / Hum** (&lt; 190 Hz): Smoothly curves left.
  - **High Pitch / Whistle** (&gt; 380 Hz): Smoothly curves right.
  - **Mid Tone / Speaking**: Moves straight ahead.
- **Optional Mouse-Aim Companion**:
  - Hovering/pointing your cursor on the canvas directs where the thief faces, while your voice provides throttle and speed!
- **Keyboard (Backup Option)**:
  - WASD or Arrow Keys can still be used if preferred. Shift triggers a manual Shout Dash.

---

## 📊 Real-Time Decibels (dB) Measurement

The game calculates true sound pressure levels using the native Web Audio `AnalyserNode`:
- **dBFS (Decibels relative to Full Scale)**: Displayed from `-90 dBFS` (silence) up to `0 dBFS` (maximum digital input).
- **dB SPL (Sound Pressure Level Approximation)**: Correlated from `25 dB SPL` (quiet bedroom) up to `100 dB SPL` (shouting).
- **Room Background Silence Calibration**: A 3-second calibration phase measures your room's ambient noise floor in decibels (e.g., `-54 dBFS`) so normal room silence reads as 0 noise.
- **HUD Decibel Gauge**: Live readout in the header and HUD bar shows your exact decibels every frame.

---

## 📹 Voice Video Mode (Webcam Picture-in-Picture)

- Click **&ldquo;📷 Toggle Voice Video&rdquo;** to activate a Picture-in-Picture webcam feed right in the top-right corner of the canvas.
- Features:
  - Live video overlay displaying your current decibels (`dB`) and active steering action.
  - Real-time video motion tracking: tilt or move your head left/right to steer the thief hands-free!

---

## 🕹️ Stealth Heist Mechanics & 3 Levels

- **Noise Radius Circle**: A soft glowing ring around the thief grows larger as your decibels rise.
- **Guards & Hearing**:
  - If a guard is inside your noise circle, they hear you, break from their patrol, and rush to investigate the sound location!
  - After searching for 2 seconds, they resume their patrol route.
- **Vision Cones & Spotted Meter**:
  - Guards cast realistic flashlight cones that stop at walls.
  - If caught in a vision cone, the Spotted Meter fills up. Reach 100% and you are captured!
- **3 Mansion Wings**:
  - **Wing 1 (The Grand Foyer)**: 1 Guard. Steal the Royal Sapphire and escape.
  - **Wing 2 (The Royal Library)**: 2 Guards with intersecting patrols. Steal the Emerald Codex.
  - **Wing 3 (The Master Vault)**: 3 Guards in security corridors. Claim the Crown of Whispers and reach extraction!
  - *The exit gate is locked with iron bars and opens only once the loot is stolen.*
- **Best Time**: Saved automatically in browser `localStorage`.

---

## 🚀 Running Locally

Because browsers require a secure context (`http://localhost` or `https://`) for microphone and webcam access:

### Option A: Using Python (Recommended)
```bash
python -m http.server 8080
```
Then open:
```
http://localhost:8080
```

### Option B: Using Node.js
```bash
npx -y serve .
```
Then navigate to the URL printed in the terminal.

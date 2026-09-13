# COLMAP Pipeline

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/opsabove)

A GUI tool for running COLMAP photogrammetry pipelines optimized for drone footage and 3D Gaussian Splatting workflows with [LichtFeld Studio](https://lichtfeld.io).

<img width="1917" height="1129" alt="screenshot" src="https://github.com/user-attachments/assets/afe40f58-5e47-4303-9049-5d0958dc8b86" />


---

## Features

- **GPS-aware reconstruction** — uses `pose_prior_mapper` with spatial matching when GPS EXIF is present
- **Sequential matching** — for indoor or GPS-denied scenes (time-interval captured footage)
- **Flat / Perspective and Raw Fisheye** camera model support
- **Stop & Resume** — safely interrupt and continue from the last completed step
- **Auto-resume detection** — detects which pipeline step to resume from automatically
- **Images junction** — automatically links your images folder inside the workspace so LichtFeld Studio resolves them correctly
- **Config persistence** — remembers your last paths and settings

---

## Requirements

- Windows 10 / 11 (64-bit)
- [LichtFeld Studio](https://lichtfeld.io) — COLMAP is bundled inside

---

## Installation

Download the latest release from the [Releases](../../releases) page and run the installer.

The installer places **COLMAP Pipeline** alongside LichtFeld Studio and adds shortcuts to your Desktop and Start Menu.

---

## Usage

### 1. Set paths

| Field | Description |
|---|---|
| **LichtFeld Studio** | Root folder of your LichtFeld Studio installation |
| **Images Folder** | Folder containing your exported frames (GPS EXIF recommended) |
| **Work Folder** | Output directory — will contain `database.db`, `sparse/`, and an `images` link |

### 2. Choose settings

**Frame type**

| Option | When to use |
|---|---|
| Flat / Perspective | Frames extracted with a frame export tool (reprojected virtual cameras) |
| Raw Fisheye | Unprocessed fisheye frames |

**GPS / Location**

| Option | When to use |
|---|---|
| GPS in EXIF | Outdoor flights with GPS telemetry — enables spatial matching and `pose_prior_mapper` |
| No GPS — Sequential | Indoor scenes or GPS-denied environments |

### 3. Run

Click **Run COLMAP**. Progress is shown in real time in the log panel.

- **Stop** — safely terminates the current step
- **Resume** — continues from the last completed step without restarting
- **Open Output** — opens the work folder in Explorer when done

### 4. Import into LichtFeld Studio

Drag the work folder into LichtFeld Studio to start 3DGS training.

---

## Pipeline steps

```
[1/3] Feature Extraction   →  SIFT features per image
[2/3] Feature Matching     →  spatial_matcher (GPS) or sequential_matcher
[3/3] Reconstruction       →  pose_prior_mapper (GPS) or mapper
```

---

## Recommended workflow

Extract frames from your drone footage using any frame export tool that writes GPS EXIF metadata. For best results, export perspective (flat) frames with GPS tags from the original telemetry.

```
Drone footage
        ↓
Frame export tool  →  GPS-tagged frames
        ↓
COLMAP Pipeline  →  sparse reconstruction
        ↓
LichtFeld Studio  →  3D Gaussian Splatting
```

---

## License

MIT — see [LICENSE](LICENSE)

---

<p align="center">
  Made with ☕ by <a href="https://www.opsabove.com">OpsAbove</a> ·
  <a href="https://ko-fi.com/opsabove">Support on Ko-fi</a>
</p>

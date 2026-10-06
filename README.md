# Bravo Pipetting Map Designer

A lightweight, responsive, single-page web application to design liquid handling pipetting maps for an **Agilent Bravo liquid handler** (specifically for reformatting, aliquoting, and pooling workflows).

![Bravo Pipetting Map Designer](https://img.shields.io/badge/Agilent_Bravo-Liquid_Handling-0066cc?style=flat-square)
![96-Well Plate](https://img.shields.io/badge/Labware-96--Well_SBS-green?style=flat-square)
![No Dependencies](https://img.shields.io/badge/Dependencies-Zero-blue?style=flat-square)

---

## Table of Contents
- [Features](#features)
- [Installation & Quick Start](#installation--quick-start)
- [How to Use](#how-to-use)
  - [1. Setting Transfer Volume](#1-setting-transfer-volume)
  - [2. Multi-Dispense Mode (Aliquoting)](#2-multi-dispense-mode-aliquoting)
  - [3. Pooling Workflow](#3-pooling-workflow)
  - [4. Overflow Protection](#4-overflow-protection)
  - [5. Well Inspector & Editing](#5-well-inspector--editing)
  - [6. Exporting to Agilent Bravo](#6-exporting-to-agilent-bravo)
- [CSV Output Format](#csv-output-format)
- [Deploying to GitHub Pages](#deploying-to-github-pages)

---

## Features

- **Standard 96-Well Microplate Arrays (ANSI/SLAS)**:
  - 8 rows labeled `A` through `H`, 12 columns labeled `1` through `12`.
  - Authentic SBS microplate bezel styling with orientation chamfer (`A1` notch).
  - Side-by-side **Source Plate** and **Destination / Final Plate**.
- **Interactive Mapping & Multi-Dispense**:
  - Click a source well to select it, then click destination wells to route transfers.
  - Multi-dispense mode toggle for rapid 1-to-many aliquoting.
  - Supports pooling multiple source wells into the same destination well.
- **Volume & Overflow Monitoring**:
  - Configurable transfer volume per step (µL).
  - Real-time running total volume calculated per destination well.
  - Dynamic liquid level indicators with automated warning alerts when volume exceeds standard 96-well capacity (~300 µL).
- **Well Inspector & Script Output**:
  - Live preview formatted strictly for Agilent Bravo transfer scripts: `[SourceWell], [DestinationWell], [Volume]`.
  - Inspector side-panel to view details and delete individual transfer steps.
  - One-click **Copy CSV** and **Download .csv**.

---

## Installation & Quick Start

The application is completely self-contained in a single HTML file with **zero local build steps or package dependencies**.

### Option 1: Open Directly in Browser (Easiest)

1. Clone or download the repository:
   ```bash
   git clone https://github.com/zcays/bravo-mapper.git
   cd bravo-mapper
   ```

2. Open `index.html` in your web browser:
   - **macOS**:
     ```bash
     open index.html
     ```
   - **Linux**:
     ```bash
     xdg-open index.html
     ```
   - **Windows**:
     ```cmd
     start index.html
     ```
   *(Or simply double-click `index.html` in your file explorer.)*

### Option 2: Run with a Local Web Server

If you prefer running through a local development server:

- **Using Python 3**:
  ```bash
  python3 -m http.server 8000
  ```
  Then navigate to `http://localhost:8000`.

- **Using Node.js**:
  ```bash
  npx serve .
  ```

---

## How to Use

### 1. Setting Transfer Volume
- Locate the **Volume (µL)** input in the top header.
- Enter the desired aspiration/dispense volume (default is `50` µL, minimum `0.5` µL, step size `0.5` µL).
- You can adjust this volume at any time between transfer steps.

### 2. Basic Transfer & Multi-Dispense Mode (Aliquoting)
1. **Single Transfer Mode** (Default):
   - Click a well on the **Source Plate** (e.g., `A1`). The well highlights with a blue active glow.
   - Click a well on the **Destination Plate** (e.g., `B2`).
   - The transfer is recorded and the source selection resets.
2. **Multi-Dispense Mode (Aliquoting)**:
   - Toggle **Multi-dispense mode** ON in the top header.
   - Click a source well once (e.g., `A1`).
   - Click multiple destination wells sequentially (e.g., `B1`, `B2`, `B3`, `B4`).
   - Each click immediately registers a transfer of the specified volume without needing to reselect `A1`.

### 3. Pooling Workflow
- To pool liquid from multiple sources into a single target well:
  1. Select Source Well `A1` &rarr; click Destination Well `C3`.
  2. Select Source Well `B2` &rarr; click Destination Well `C3`.
  3. Select Source Well `D4` &rarr; click Destination Well `C3`.
- The destination well accumulates liquid and displays a combined volume total.

### 4. Overflow Protection
- Standard 96-well microplates generally have a working volume of **200–300 µL**.
- Destination wells display a rising green liquid fill animation proportional to the volume added.
- If the accumulated volume in any destination well exceeds **300 µL**, the well turns **red with a pulsing warning animation** and updates its hover tooltip to alert against well overflow.

### 5. Well Inspector & Editing
- Click on any mapped source or destination well at any time to open the **Well Inspector** in the sidebar.
- The inspector displays:
  - Well identity (Source or Destination).
  - Total liquid volume accumulated.
  - Chronological list of transfers involving that well.
  - A **trash icon** next to each transfer step allowing you to delete unwanted actions without restarting.

### 6. Exporting to Agilent Bravo
- **Live Script Area**: Continuously displays the formatted pipetting commands.
- **Copy CSV**: Copies the mapping directly to your clipboard for pasting into spreadsheets or VWorks.
- **Download**: Saves a ready-to-use `pipetting_map.csv` file to your computer.
- **Clear All Mappings**: Resets both plates and starts a clean design.

---

## CSV Output Format

The output strictly complies with standard liquid handling hit-pick and reformatting mapping matrices:

```csv
[SourceWell], [DestinationWell], [Volume]
```

### Example:
```csv
A1, A1, 100
A2, A2, 200
B1, C3, 50
B2, C3, 50
```

This format can be directly imported into **Agilent VWorks** pipetting hit-pick tasks or custom automation scripts.

---

## Deploying to GitHub Pages

To make this application accessible via the web for your lab team without local installation:

1. Go to your repository on GitHub: `https://github.com/zcays/bravo-mapper`
2. Navigate to **Settings** &rarr; **Pages** (in the left sidebar).
3. Under **Build and deployment**:
   - Source: **Deploy from a branch**
   - Branch: **`main`** / Folder: **`/ (root)`**
4. Click **Save**.
5. Your application will be live at:
   ```
   https://zcays.github.io/bravo-mapper/
   ```

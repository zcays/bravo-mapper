# Bravo Pipetting Map Designer

A lightweight, responsive, single-page web application to design liquid handling pipetting maps for an **Agilent Bravo liquid handler** (specifically for reformatting and pooling workflows).

## Features

- **Standard 96-Well Microplate Arrays (ANSI/SLAS)**:
  - 8 rows labeled `A` through `H`, 12 columns labeled `1` through `12`.
  - Realistic SBS microplate bezel styling with orientation chamfer (`A1` notch).
  - Side-by-side **Source Plate** and **Destination / Final Plate**.
- **Interactive Mapping & Multi-Dispense**:
  - Click a source well to select it, then click destination wells to route transfers.
  - Multi-dispense mode toggle for aliquoting from a single source to multiple destinations.
  - Supports pooling multiple source wells into the same destination well.
- **Volume & Overflow Monitoring**:
  - Configurable transfer volume per step (µL).
  - Real-time running total calculation per destination well.
  - Animated liquid level indicators with automated warning states when volume exceeds ~300 µL.
- **Well Inspector & Script Output**:
  - Live preview formatted strictly for Agilent Bravo transfer scripts: `[SourceWell], [DestinationWell], [Volume]`.
  - Inspector side-panel to review and delete individual steps.
  - One-click **Copy CSV** and **Download .csv**.

## Getting Started

Simply open `index.html` in any modern web browser:
```bash
open index.html
```
No build steps or dependencies required.

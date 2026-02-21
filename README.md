# Flaking Experiments Web App

A cross-platform web application for collecting data during randomized quartz clast reduction experiments. Designed for use in laboratory settings on any device — iPad, laptop, or desktop.

**Live app:** [https://jmcascalheira.github.io/FlakingExperimentsWeb/](https://jmcascalheira.github.io/FlakingExperimentsWeb/)

## Overview

This app guides experimenters through a structured workflow for recording variables during controlled flaking experiments. It tracks platform states across strikes, generates random platform selections, and exports all data as a single CSV file ready for analysis.

The app was built to support the experimental protocol described in Ferar et al. (in prep), which defines a standardized set of variables for randomized flaking experiments on quartz clasts.

## Features

- **6-tab workflow**: Experiment Details → Platform Setup → Random Platform → Platform Changes → Post-Strike Data → End Experiment
- **Random platform selection**: Randomly selects from available platforms for each strike
- **Platform tap-cycling**: Tap platforms to cycle their status (Available → Removed by Flake → Removed by Fragment)
- **Unviable platform handling**: Mark platforms as unviable after failed strike attempts, with automatic re-selection
- **3D scan reminders**: Prompts every 3rd strike to create a 3D model of the core
- **Single CSV export**: All experiment-level and strike-level data in one file, including per-platform status snapshots
- **Auto-save**: Data is automatically saved to browser storage after every strike
- **Folder auto-save** (Chrome/Edge): Optionally select a folder and the CSV updates automatically after each strike — no manual export needed
- **Offline support**: Works without internet when installed to the home screen
- **Cross-platform**: Runs on any device with a modern web browser

## Installation

### As a web app (recommended)

Simply open the [live app URL](https://jmcascalheira.github.io/FlakingExperimentsWeb/) in any modern browser.

### On iPad (Add to Home Screen)

1. Open the URL in **Safari**
2. Tap the **Share** button (square with arrow)
3. Select **"Add to Home Screen"**
4. The app will appear as an icon and work offline

### Local use

Download or clone the repository and open `index.html` in any browser:

```bash
git clone https://github.com/jmcascalheira/FlakingExperimentsWeb.git
open FlakingExperimentsWeb/index.html
```

## Workflow

1. **Experiment Details** — Enter experiment number, date, clast information, and notes. Optionally select an auto-save folder (Chrome/Edge only).
2. **Platform Setup** — Set the initial number of platforms using +/− buttons.
3. **Random Platform** — Generate a random platform selection. Record platform quality, location, and type. Mark unviable if needed.
4. **Platform Changes** — Tap platforms to record status changes from this strike. Add new platforms created by the blow.
5. **Post-Strike Data** — Record hammerstone info, blow success, platform type counts, core weight, fragmentation, and notes.
6. **End Experiment** — Record final core weight, debris weight, and stone quality rating. Export the complete dataset.

Steps 2–5 repeat for each strike until the experiment is ended.

## Data Output

The app exports a single CSV file with all variables. Each row represents one strike (or an unviable platform attempt), with experiment-level details repeated on every row for easy analysis.

### CSV columns

| Column | Description |
|--------|-------------|
| `Experiment_Number` | Experiment identifier |
| `Date` | Experiment date |
| `Clast_Number_ID` | Clast identifier |
| `Clast_Source_ID` | Clast source identifier |
| `Clast_Weight_g` | Initial clast weight in grams |
| `Clast_Notes` | Notes about the clast |
| `Final_Core_Weight_g` | Final core weight (end of experiment) |
| `Debris_Weight_g` | Debris weight (end of experiment) |
| `Stone_Quality_Rating` | Overall stone quality (1–5) |
| `Strike` | Strike/blow number |
| `RandomPlatform` | Randomly selected platform ID |
| `Platform_Quality` | Platform quality rating (1–5) |
| `Platform_Location` | Platform location (Position 1–7) |
| `Platform_Type` | Platform type (Cortical, Flaw Cortex, Fracture Surface, Plain, Dihedral) |
| `Platforms_Pre_Blow` | Number of platforms before this blow |
| `Platforms_Created` | Number of new platforms created by this blow |
| `Platforms_Removed_Flake` | Platforms removed by flake this blow |
| `Platforms_Removed_Fragment` | Platforms removed by fragment this blow |
| `Hammerstone_ID` | Hammerstone identifier |
| `Hammerstone_Failure` | Hammerstone failure type (None, Chipping, Failure) |
| `Blow_Success` | Blow success rating (0–5) |
| `Unifacial_Simple` | Unifacial simple platform count |
| `Unifacial_Abrupt` | Unifacial abrupt platform count |
| `Bifacial_Simple` | Bifacial simple platform count |
| `Bifacial_Abrupt` | Bifacial abrupt platform count |
| `Core_Weight_g` | Core weight after this strike |
| `Core_Fragmentation` | Whether fragmentation occurred |
| `Fragment_Number` | Number of fragments |
| `Fragment_Weight_g` | Fragment weight in grams |
| `Strike_Notes` | Notes for this strike |
| `Platform_1`, `Platform_2`, ... | Per-platform status snapshot (A = Available, AX = Removed by Flake, AF = Removed by Fragment, B = Previously removed, empty = not yet created) |

## Platform Status Codes

| Code | Meaning |
|------|---------|
| **A** | Available — platform exists and can be selected |
| **AX** | Removed by Flake — platform was knocked off by a flake during this blow |
| **AF** | Removed by Fragment — platform was knocked off by a fragment during this blow |
| **B** | Gone — platform was removed in a previous strike |
| *(empty)* | Platform did not exist yet at this point |

## Browser Compatibility

| Feature | Chrome/Edge | Safari | Firefox |
|---------|:-----------:|:------:|:-------:|
| Core app | ✅ | ✅ | ✅ |
| CSV download | ✅ | ✅ | ✅ |
| Offline (home screen) | ✅ | ✅ | ✅ |
| Auto-save to folder | ✅ | ❌ | ❌ |

The auto-save to folder feature uses the [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API), which is currently supported in Chromium-based browsers only. On all browsers, data is always saved to browser local storage as a backup.

## Native App Alternative

A native SwiftUI version of this app (macOS/iOS) is available in the [core_experiments_shiny](https://github.com/jmcascalheira/core_experiments_shiny) repository under `FlakingExperiments/`.

## License

MIT

## Citation

If you use this app in your research, please cite:

Ferar, N., Cascalheira, J. (in prep). *Randomized flaking experiments on quartz clasts: protocol and data collection tools.*

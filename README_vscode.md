# MAE223 — Week 1: Time Series Analysis
### VS Code Setup Guide (no terminal required after Miniconda)

This guide walks through the complete setup using VS Code's built-in tools. After installing Miniconda, you will not need to open a terminal — cloning, environment creation, and all Git operations are handled inside VS Code.

---

## Files

| File | Description |
|------|-------------|
| `Tidal Analysis_Python.ipynb` | **Start here** — fully written demo notebook |
| `Tutorial_SpectralAnalysis.ipynb` | **Then here** — hands-on tutorial, you write the code |
| `sample_data.json` | Velocity time series (CLASS10 mooring, 30-min sampling, 16,000 samples) |
| `la_jolla_tide.json` | NOAA La Jolla tide gauge sea level — full ~100-year record, hourly, in mm |
| `safari_waves.json` | SAFARI buoy significant wave height — central Pacific, Nov 2025–Apr 2026, ~2-hr sampling (Scripps/WHOI collaboration) |
| `environment.yml` | Conda environment specification |
| `github_tutorial.pdf` | Guide to GitHub and GitHub Classroom for first-time users |

---

## Setup (do this once)

### Step 0 — Create a GitHub account

You need a free GitHub account to access this assignment.

1. Go to [github.com](https://github.com) and click **Sign up**
2. Enter your email, a password, and a username
   - Your username will be visible to your instructor — keep it professional
   - Using your UCSD email is recommended but not required
3. Verify your email address when prompted
4. Once your account is active, click the assignment link posted on Canvas
5. Click **Accept this assignment** — GitHub Classroom will create a personal copy of this repository just for you
6. Wait a few seconds, then refresh — you will see a link to your own repo

> Your repo is an independent copy. Changes you make do not affect anyone else's, and no other student can see yours.

---

### Step 1 — Install Miniconda

Miniconda is the only step that requires going outside VS Code. It installs `conda`, the package manager that VS Code uses to create your Python environment.

**Skip this step if you already have Anaconda or Miniconda installed.**

**Mac:**
1. Go to https://docs.conda.io/en/latest/miniconda.html
2. Download the **macOS** installer — choose **Apple Silicon** for M1/M2/M3/M4 Macs, or **Intel** otherwise
3. Open the downloaded `.pkg` file and follow the prompts
4. To verify: open a Terminal (`Cmd+Space` → type `Terminal`), type `conda --version`, and press Enter — you should see something like `conda 24.x.x`

**Windows:**
1. Go to https://docs.conda.io/en/latest/miniconda.html
2. Download the **Windows 64-bit** installer (`.exe`)
3. Run the installer. When you reach the **Advanced Options** screen, check **"Add Miniconda3 to my PATH environment variable"**
4. Click through the remaining prompts and finish
5. To verify: open **Anaconda Prompt** from the Start menu, type `conda --version`, and press Enter

---

### Step 2 — Install VS Code

1. Download and install VS Code from https://code.visualstudio.com
2. Open VS Code and go to the **Extensions** panel — click the square icon on the left sidebar or press `Cmd+Shift+X` (Mac) / `Ctrl+Shift+X` (Windows)
3. Search for **Python** and click Install
4. Search for **Jupyter** and click Install
5. Restart VS Code after both extensions finish installing

---

### Step 3 — Clone your repository inside VS Code

No terminal needed — VS Code can clone directly from GitHub.

1. Open VS Code
2. Click the **Source Control** icon on the left sidebar (branch icon) or press `Cmd+Shift+G` (Mac) / `Ctrl+Shift+G` (Windows)
3. Click **Clone Repository**
4. Click **Clone from GitHub** — VS Code will prompt you to sign in to GitHub if you haven't already. Follow the browser prompt to authorize VS Code.
5. Type your repository name (e.g. `time-series-analysis-yourname`) in the search box, or paste the full URL from your GitHub Classroom repo page
6. Choose a folder on your computer to save it into and click **Select as Repository Destination**
7. When prompted, click **Open** to open the cloned repo in VS Code

---

### Step 4 — Create the course Python environment

**Try the VS Code GUI method first (all platforms):**

1. Make sure the repo folder is open — check the Explorer panel on the left sidebar and confirm you can see `environment.yml` in the file list. If not, go to **File → Open Folder**, select your `time-series-analysis` folder, then continue.
2. Open the **Command Palette**: press `Cmd+Shift+P` (Mac) / `Ctrl+Shift+P` (Windows)
3. Type `Python: Create Environment` and select it
4. Choose **Conda**
5. Select `environment.yml` when prompted
6. Wait a few minutes — a progress bar will appear at the bottom of VS Code
7. When it finishes, VS Code will register `mae223` as an available kernel automatically

**If nothing happens after selecting Conda (common on Windows), use the terminal fallback:**

1. Open the VS Code integrated terminal: press `` Ctrl+` `` (backtick) or go to **Terminal → New Terminal**
2. Run these three commands one at a time, pressing Enter after each:
```
conda env create -f environment.yml
conda activate mae223
python -m ipykernel install --user --name mae223 --display-name "mae223"
```
3. Close and reopen VS Code when the commands finish

> **Windows tip:** If `conda` is not recognised in the VS Code terminal, close VS Code, open **Anaconda Prompt** from the Start menu, navigate to your repo folder with `cd path\to\time-series-analysis`, and run the three commands above from there instead.

---

### Step 5 — Open the notebooks

There are two notebooks and they should be done **in order**:

**1. `Tidal Analysis_Python.ipynb` — demo (start here)**
- Fully written — just run it and read the code and output
- Introduces the `spectrumCB` function, power spectral density, and tidal analysis
- No coding required — this is the "watch and understand" step

**2. `Tutorial_SpectralAnalysis.ipynb` — tutorial (do this second)**
- You write the code yourself, guided by prompts
- Builds directly on what the demo introduced
- Requires `la_jolla_tide.json` and `safari_waves.json` (both included in the repo)

The tutorial has two parts:

**Part 1 — Spectral Resolution**
Using the La Jolla tide gauge record, you will compute spectra with four different chunk sizes and compare them on a single plot. The goal is to build intuition for the tradeoff between frequency resolution and spectral stability — a core concept in Welch's method. Three reflection questions guide your interpretation, including a calculation of the minimum segment length needed to resolve the M₂ and S₂ tidal constituents.

**Part 2 — SAFARI Wave Analysis**
You will apply the full analysis pipeline to a new dataset: significant wave height (Hs) measured by a research buoy in the central North Pacific (33°25'N, 158°W) during the SAFARI 2025–2026 field campaign — a joint Scripps Institution of Oceanography and Woods Hole Oceanographic Institution (WHOI) collaboration. The data are transmitted via Iridium satellite and are irregularly sampled, so you will need to interpolate onto a regular time grid before computing the spectrum. You will then identify the dominant periods of wave height variability and compare the result to the tidal spectrum from the demo.

> **How to work through the tutorial:** Each code cell either contains fully written code (run it and read it) or has a `# YOUR CODE HERE` comment where you must write something. Read the markdown cells carefully before each exercise — they explain what you need to do and why. Answer the reflection questions in the provided answer cells.

**To open a notebook:**
1. Click the notebook file in the left file panel
2. In the top-right corner click **Select Kernel → Python Environments... → mae223**
3. Click **Run All** to execute all cells

> **Note:** Always run cells from top to bottom. If you see a `NameError`, it usually means an earlier cell has not been run yet. Use **Run All** to avoid this.

---

### Step 6 — Save your work to GitHub

Push your changes to GitHub periodically as you work — this keeps your code backed up and lets you pick up where you left off from any computer.

1. Open the **Source Control** panel (`Cmd+Shift+G` / `Ctrl+Shift+G`)
2. Changed files appear under **Changes** — click the `+` next to the file to stage it
3. Type a short message describing what you did (e.g. `completed tidal spectrum section`) and click **Commit**
4. Click **Sync Changes** to push to your GitHub repo

You can push as many times as you like — each push saves a snapshot of your progress.

> **Note:** Lab reports are submitted through Canvas, not GitHub.

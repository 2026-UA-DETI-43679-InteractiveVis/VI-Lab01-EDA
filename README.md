# Interactive Visualization - Lab 01: Environment Setup

This document explains how to set up your Python environment and install all required packages before the lab session.

---

## Requirements

- **Python 3.10 or higher** (3.11 recommended or live wildly and go for the latest one. I have not tested it...)
- **pip** (comes bundled with Python)
- A code editor with Jupyter notebook support — [VS Code](https://code.visualstudio.com/) with the [Jupyter extension](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) is recommended

---

## Step 1: Create a virtual environment

It is strongly recommended to work inside a virtual environment to avoid conflicts with other Python projects on your machine.

Open a terminal in the folder where you will work and run:

```bash
# Create the environment (only needed once)
python -m venv .venv
```

Then activate it:

```bash
# On Windows
.venv\Scripts\activate

# On macOS / Linux
source .venv/bin/activate
```

You should see `(.venv)` appear at the start of your terminal prompt. **You need to activate the environment every time you open a new terminal.**

---

## Step 2: Install required packages

With the environment active, run the following commands:

```bash
# Core data libraries
pip install "numpy<2.0"
pip install pandas matplotlib seaborn

# Automated EDA and profiling
pip install sweetviz

# Interactive dataframe explorer
pip install dtale

# Jupyter notebook support
pip install notebook ipykernel
```

> **Why `numpy<2.0`?** Several packages (including dtale and sweetviz) are not yet fully compatible with NumPy 2.x. Pinning to a 1.x version avoids runtime errors that can be difficult to diagnose.

Alternatively, you can install everything in a single command:

```bash
pip install "numpy<2.0" pandas matplotlib seaborn sweetviz dtale notebook ipykernel
```

---


## Step 3: Verify the installation

Run the following in a terminal (with the environment active) to confirm everything is working:

```bash
python -c "
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import sweetviz as sv
import dtale
import numpy as np
print('numpy   :', np.__version__)
print('pandas  :', pd.__version__)
print('seaborn :', sns.__version__)
print('sweetviz: OK')
print('dtale   : OK')
print('All packages installed successfully.')
"
```

---

## Step 4: D-Tale in VS Code (Windows)

D-Tale opens in a browser tab via a local server. On Windows, VS Code may not automatically forward the port if D-Tale binds to a network adapter other than the loopback address. All lab notebooks already include the correct launch code:

```python
d = dtale.show(df, host='127.0.0.1', subprocess=False, open_browser=False)
print('Open D-Tale at:', d._url)
```

If the URL does not open automatically, copy it from the output and paste it into your browser. If the page does not load, check the **Ports** panel at the bottom of VS Code and confirm port `40000` is being forwarded.

---

## Files for this lab

| File | Description |
|---|---|
| `lab01_task1_datasets.ipynb` | Task 1 — Datasaurus Dozen: why visualisation is essential |
| `lab01_task2_telemetry.ipynb` | Task 2 — Guided EDA and cleaning of game telemetry data |
| `lab01_task3_git_activity.ipynb` | Task 3 — Independent EDA and cleaning of Git classroom activity data |
| `datasaurus.csv` | Dataset for Task 1 |
| `dataset_A_indie_game_telemetry.csv` | Dataset for Task 2 |
| `dataset_D_git_classroom_activity.csv` | Dataset for Task 3 |

---

## Troubleshooting

**`ModuleNotFoundError` when running a notebook**  
The notebook is using a different Python kernel, not the one from your virtual environment. In VS Code, click the kernel name in the top right of the notebook and select **Python (lab02)**.

**NumPy version conflict errors**  
Make sure you installed `numpy<2.0` as described in Step 2. If you already have a newer version, downgrade with:
```bash
pip install "numpy<2.0" --force-reinstall
```

# Phishing Email Detection Model (VS Code Project)

A Scikit-learn project that classifies emails as **Phishing** or **Safe**,
structured as a proper VS Code workspace.

## Folder structure
```
phishing_vscode_project/
├── .vscode/
│   ├── settings.json      # Python path config
│   └── launch.json        # Run/Debug configs (F5 menu)
├── src/
│   ├── generate_dataset.py   # creates the synthetic dataset
│   ├── phishing_detector.py  # trains + evaluates the model
│   └── check_email.py        # check any email interactively
├── data/
│   └── emails_dataset.csv    # generated dataset (created by step 1)
├── output/
│   ├── confusion_matrix.png  # generated after training
│   └── model.joblib, vectorizer.joblib, scaler.joblib
├── requirements.txt
└── README.md
```

## Setup in VS Code

1. **Open the folder in VS Code**: `File > Open Folder...` → select
   `phishing_vscode_project`.

2. **Install the Python extension** (if you don't have it): go to the
   Extensions tab (left sidebar, or `Ctrl+Shift+X`) and install
   **"Python"** by Microsoft.

3. **Create a virtual environment** (recommended). Open a terminal in
   VS Code (`` Ctrl+` ``) and run:
   ```bash
   python -m venv .venv
   ```
   Then select it as your interpreter: `Ctrl+Shift+P` → "Python: Select
   Interpreter" → choose `.venv`.

4. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

## Running the project

You can run each script two ways:

**Option A — Run/Debug panel (easiest):**
Click the "Run and Debug" icon in the left sidebar (▷ with a bug), pick
one of the three configs from the dropdown at the top, and press the ▷
button (or `F5`):
1. `1. Generate Dataset`
2. `2. Train & Evaluate Model`
3. `3. Check an Email`

**Option B — Terminal:**
```bash
python src/generate_dataset.py     # step 1: creates data/emails_dataset.csv
python src/phishing_detector.py    # step 2: trains model, saves to output/
python src/check_email.py          # step 3: interactively check any email
```

Run them **in this order** the first time — each step depends on the
previous one's output.

## What each script does
- **generate_dataset.py** — creates 500 synthetic emails (250 phishing,
  250 legitimate) since no real dataset was provided. Replace
  `data/emails_dataset.csv` with a real dataset any time (same `text`,
  `label` columns) and skip re-running this script.
- **phishing_detector.py** — extracts TF-IDF + hand-crafted features
  (URL count, IP-based URLs, urgency keywords, etc.), trains a Logistic
  Regression classifier, prints accuracy + confusion matrix, and saves
  the trained model to `output/`.
- **check_email.py** — loads the saved model and lets you paste any
  email text to get an instant Phishing/Safe prediction with confidence.

## Notes
- The sample dataset is synthetic (see `generate_dataset.py`). Swap in
  real data for production use.
- Re-run `phishing_detector.py` any time after changing the dataset to
  retrain and refresh the saved model.

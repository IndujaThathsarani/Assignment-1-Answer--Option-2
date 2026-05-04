# Pixels Suite — PNG preview automation (IT3040 Option 2)

This project runs a single Playwright scenario: open a Pixels Suite tool in the browser, upload a PNG, and verify that a preview region shows image-like content. Results are appended to `execution_results.csv` and a screenshot is saved under `results/`.

## Prerequisites

- **Python** 3.11 or 3.12 (64-bit recommended)
- **Google Chrome** is optional; Playwright installs and uses **Chromium** by default when you run `playwright install`

## One-time setup

1. Clone or copy this folder to your machine.

2. Open a terminal in the project directory (the folder that contains `image_preview_test.py` and this `README.md`).

3. (Recommended) Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   ```

   - **Windows (PowerShell):** `.venv\Scripts\Activate.ps1`
   - **Windows (cmd):** `.venv\Scripts\activate.bat`
   - **macOS / Linux:** `source .venv/bin/activate`

4. Upgrade pip and install Python dependencies:

   ```bash
   python -m pip install -U pip
   python -m pip install -r requirements.txt
   ```

5. Install Playwright browser binaries (required once per machine):

   ```bash
   playwright install
   ```

   To install only Chromium (smaller download):

   ```bash
   playwright install chromium
   ```

## How to run the test

From the same directory as `image_preview_test.py`:

```bash
python image_preview_test.py --url "https://www.pixelssuite.com/convert-to-png" --slow-mo-ms 2000
```

- If `sample.png` is missing, the script creates a minimal 1×1 PNG automatically.
- To use your own PNG:

  ```bash
  python image_preview_test.py --png "path\to\your.png" --url "https://www.pixelssuite.com/convert-to-png"
  ```

### Optional arguments

| Argument | Description |
|----------|-------------|
| `--url` | Page to open (default: `https://www.pixelssuite.com/convert-to-png`) |
| `--png` | Path to the PNG to upload (default: `sample.png`) |
| `--csv` | Path to the results CSV (default: `execution_results.csv`) |
| `--out-dir` | Folder for screenshots (default: `results`) |
| `--headless` | Run without opening a visible browser window |
| `--timeout-ms` | Maximum time for steps in milliseconds (default: `60000`) |
| `--slow-mo-ms` | Delay between Playwright actions, in ms (default: `0`; use e.g. `2000` to watch the run) |

Example headless run:

```bash
python image_preview_test.py --headless --url "https://www.pixelssuite.com/convert-to-png"
```

## Outputs after a run

- **`execution_results.csv`** — one new row per run (columns: `file_type`, `file_path`, `preview_detected`, `status`, `screenshot`). Delete or rename the file first if you need a clean CSV with only the header plus one row for submission.
- **`results/preview_pass.png`** or **`results/preview_fail.png`** — full-page screenshot when the test finishes successfully; **`results/preview_error.png`** if an exception occurred.

## Troubleshooting

- **`playwright` not found:** Ensure the virtual environment is activated and `pip install -r requirements.txt` completed without errors.
- **Browser download fails:** Check network/firewall; retry `playwright install chromium`.
- **Upload or preview timeout:** Increase `--timeout-ms` or confirm the site loads manually in a browser.

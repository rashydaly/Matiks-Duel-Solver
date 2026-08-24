Logic Duel Solver Final Version (Manifest V3)
Logic Duel Solver Final Version is a Manifest V3 Chrome extension built to read, solve, and optionally fill mathematical puzzles directly from Matiks Logic Duel. It interacts with the live webpage DOM without relying on screenshots, image processing, or OCR.

🚀 Key Features
Direct DOM Text Extraction: Reads puzzle modes and values straight from visible text.

Split-Number Reconstruction: Automatically combines number fragments split across separate DOM elements (e.g., elements 48 and 5 combine into 485).

Spatial Text Grouping: Joins related text fragments left-to-right to read complete expressions accurately.

Power & Root Handling:

Preserves multi-digit superscript powers without truncation.

Supports square roots, cube roots, and indexed root formats

Advanced Math Operations: Supports MOD, REMAINDER, HCF, GCD, LCM, POWER, ROOT, ROOTS, SUM OF SQUARES (e.g., 14→3 2 1), and PRIME FACTORS (e.g., 12→2 2 3).

Automation Controls:

Fast Answer Filling: Inserts solutions via native input and change events.

Auto-submit: Automatically presses the Enter key after filling when enabled.

Auto Solver Mode: Monitors actual puzzle mutations to process new questions dynamically without short-interval polling.

📊 Supported Math Examples
Mode	Example	Result
MOD / REMAINDER	96 % 3	0
POWER	3^3	27
Square root	√[2] 256	16
Cube root	√[3] 27	3
Sum of squares	14	3 2 1
Prime factors	12	2 2 3
HCF / GCD	18, 24	6
LCM	6, 8	24
🛠️ Extracted Data Structure
The extractor normalizes detected puzzles into structured data objects for internal processing and diagnostics:

Standard Expression Example:

JSON
{
  "mode": "REMAINDER / MOD",
  "value": "96 % 3",
  "rawText": "REMAINDER / MOD\n96 % 3",
  "numbers": [96, 3],
  "operators": ["%"],
  "parts": ["96", "%", "3"]
}
Split-Number Example:

JSON
{
  "mode": "SOME MODE",
  "value": "485",
  "rawText": "48 5",
  "numbers": [485],
  "parts": ["485"]
}
📦 Installation Guide
Extract the extension ZIP file into a standard local folder.

Open Chrome (or any Chromium-based browser) and go to chrome://extensions/.

Enable Developer mode using the toggle in the top-right corner.

Click Load unpacked.

Select the main extracted folder where manifest.json is directly visible (do not select nested directories like icons).

Navigate to a Logic Duel match on Matiks and use the extension popup to solve or auto-fill.

🔧 Troubleshooting
Manifest Error: If Chrome reports “Manifest file is missing or unreadable”, ensure you selected the directory containing manifest.json directly, rather than an internal asset or icon subfolder.

Unrecognized Puzzle: Keep the game board visible and click Solve Now again if a puzzle element fails to register.

Observer Desync: If Auto Solver Mode behaves unexpectedly after switching matches, toggle it off and on once to reinitialize the DOM observer.

Input Not Filling: Verify that the game input field is active/visible and that both Auto-fill and Auto-submit options are appropriately toggled on in the popup.

Logic Duel Solver V1
Logic Duel Solver V1 is a Manifest V3 Chrome extension designed to read, solve, and optionally fill mathematical puzzles from Matiks Logic Duel. The extension works directly with the live webpage DOM and does not depend on screenshots, image processing, or OCR.
Key Features
Direct DOM Text Extraction: Reads the puzzle mode and mathematical values directly from visible webpage text.
Split-Number Reconstruction: Correctly combines number fragments that are stored in separate DOM elements. For example, if 485 is stored as 48 in one element and 5 in another, the extractor reconstructs the complete value as 485.
Spatial Text Grouping: Joins related text fragments in their visual left-to-right order so that split numbers, operators, and expressions are read as one complete puzzle.
Power Handling: Supports expressions such as 3^3, 16^9, and multi-digit powers without dropping the first or last digit.
Root Handling: Supports square roots, cube roots, and indexed root formats such as √[2] 256 and √[3] 27.
Sum of Squares: Supports multiple answer values, for example 14 → 3 2 1, because 3² + 2² + 1² = 14.
Prime Factorization: Returns individual prime factors separately, for example 12 → 2 2 3.
Other Math Modes: Supports MOD, REMAINDER, HCF, GCD, LCM, POWER, ROOT, ROOTS, SUM OF SQUARES, and PRIME FACTORS.
Fast Answer Filling: Detects the active game input and inserts the calculated answer through native input and change events.
Auto-submit: Can trigger the Enter key after filling when Auto-submit is enabled.
Auto Solver Mode: Watches for actual puzzle changes and processes a new question without repeatedly scanning the page at a fixed short interval.
How Split Numbers Are Read
Some puzzle values are not stored as one complete text value. The game may split a number across multiple neighboring DOM elements. For example:
text
DOM element 1: 48
DOM element 2: 5
Actual number: 485
The extractor identifies nearby related fragments and combines them in their visual order:
text
48 + 5 → 485
This prevents incomplete extraction such as reading only 48 or only 5.
The same reconstruction method can be used for longer values and expressions when the game stores different portions separately, such as:
text
125 + 60 = 185
The extension preserves the complete value and the correct order of numbers and operators before passing the expression to the solver.
Supported Math Examples
Mode
Example
Result
MOD / REMAINDER
96 % 3
0
POWER
3^3
27
Square root
√[2] 256
16
Cube root
√[3] 27
3
Sum of squares
14
3 2 1
Prime factors
12
2 2 3
HCF / GCD
18, 24
6
LCM
6, 8
24
Root and Power Logic
The extension uses the actual mathematical structure detected in the puzzle. A normal number is not automatically treated as a power merely because its digits can be divided into groups. For example, an ordinary number such as 485 remains 485 and is not incorrectly interpreted as 48^5 unless an actual power marker is present.
Standard indexed root notation is handled as follows:
text
√[2] 256 → 16
√[3] 27  → 3
For rendered root formats where the degree marker and target value are stored separately, the solver supports the corresponding bracket and degree pattern. Exact square or cube roots are preferred, and the appropriate fallback is used only when the first interpretation does not produce a valid result.
For superscript powers, complete multi-digit values are preserved before calculation. This prevents errors such as reading 66² as 6².
Auto Solver, Auto-fill, and Auto-submit
Click Solve Now to read and solve the current puzzle once. The calculated answer is displayed in the extension popup.
When Auto Solver Mode is enabled, the extension monitors relevant DOM changes. When a new question appears, it scans the updated puzzle and displays the new solution. Duplicate scans for the same puzzle are ignored.
When Auto-fill is enabled, the solution is inserted into the active game input. When Auto-submit is enabled, the extension also sends the Enter key after filling. If Auto-fill is disabled, the answer is calculated and displayed without changing the game input.
Extracted Data
The extractor normalizes the detected puzzle into a data object similar to this:
js
{
  mode: "REMAINDER / MOD",
  value: "96 % 3",
  rawText: "REMAINDER / MOD\n96 % 3",
  numbers: [96, 3],
  operators: ["%"],
  parts: ["96", "%", "3"]
}
For a split number, the final normalized value is reconstructed before solving:
js
{
  mode: "SOME MODE",
  value: "485",
  rawText: "48 5",
  numbers: [485],
  parts: ["485"]
}
The value field is the primary input used by the math solver. The remaining fields are retained for diagnostics and integration.
Installation
Extract the extension ZIP into a normal folder.
Open chrome://extensions/ in Chrome or another Chromium-based browser.
Enable Developer mode.
Click Load unpacked.
Select the extracted main extension folder in which manifest.json is directly visible.
Do not select a nested folder such as icons or any other asset folder.
Open a Logic Duel match on https://www.matiks.com/.
Open the extension popup and use Solve Now, Fill Answer, or Auto Solver Mode.
Permissions
The extension uses the permissions required for the supplied build, including activeTab, scripting, and storage. It works with the configured Matiks Logic Duel page and does not send puzzle data to an external OCR or solver service.
Troubleshooting
If Chrome reports “Manifest file is missing or unreadable”, select the extracted folder where manifest.json is directly visible. Do not select the icons folder or another nested folder.
If a number is displayed across multiple DOM elements, the extractor combines neighboring fragments in visual order. If a puzzle is not detected, keep the game board visible and press Solve Now again.
If Auto Solver Mode was enabled before navigating to another match, turn it off and on once to reinitialize the page observer.
If the answer is displayed but not filled, confirm that the game input is visible and that Auto-fill is enabled. Auto-submit requires its corresponding option to be enabled.
Compatibility
The extension depends on the DOM structure and text layout used by the supplied Matiks Logic Duel build. If the website changes its element structure, text grouping, or input controls, a targeted compatibility update may be required.
Version: Logic Duel Solver V1 — Manifest V3

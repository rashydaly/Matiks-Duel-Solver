# Logic Duel Solver V1

**Logic Duel Solver V1** is an advanced Manifest V3 Chrome extension built specifically for automated puzzle extraction, real-time DOM analysis, and seamless auto-filling on Matiks Logic Duel games. 

Designed as a high-performance alternative to traditional OCR tools, it features a robust Direct DOM Extractor that parses mathematical layouts live from the webpage.

---

## Key Features

* **Direct DOM Extraction Engine:** Instantly scans and captures puzzle modes and mathematical expressions straight from live DOM nodes without image processing delays.
* **Advanced KaTeX & Power Parsing:** Safely handles complex multi-digit base numbers and superscript exponents (e.g., matching structures inside `.msupsub`, `.mord`, and `.mtight` classes) to prevent digit truncation or duplication.
* **SVG Radical & Root Recognition:** Detects visual radical symbols and normalizes custom-indexed roots accurately into clean formats (e.g., parsing square and cube roots as `√[index] value`).
* **Spatial Line Grouping:** Combines multi-token horizontal text elements sequentially from left to right to build accurate mathematical expressions.
* **Smart Auto-Filler & Auto-Submit:** Automatically detects active game input fields, populates calculated solutions, and simulates keyboard events (`Enter`) for instant submission.
* **Continuous Auto-Watch Mode:** Features a background polling timer to monitor live puzzle state changes and execute automated gameplay workflows.

---

## Recent Updates & Changes

* **Enhanced KaTeX Exponent Handling:** Fixed nested node concatenation issues to flawlessly capture large multi-digit bases with superscripts (e.g., handling complex power blocks without missing trailing digits).
* **Targeted Root Detection:** Optimized radical extraction logic to trigger strictly when root elements are present on screen, preventing conflicts with standard arithmetic modes like HCF, LCM, or Modulus.
* **Optimized Payload Structure:** Standardized extracted data objects to expose clean tokens, raw text, and separated arrays for numbers, operators, and root parameters to integrate smoothly with solver modules.

---

## Installation & Setup

1. Open Google Chrome and go to `chrome://extensions/`.
2. Enable **Developer mode** using the toggle in the top-right corner.
3. Click **Load unpacked** and select your extension directory.
4. Open a match on `https://www.matiks.com/` and use **Solve Now** or enable **Auto Solver Mode**.

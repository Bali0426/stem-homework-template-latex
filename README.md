# stem-homework-template-latex
A template for stem homeworks written in latex.

# Antigravity LaTeX Template Specification: BME Engineering & Control Systems Report

## 1. Document Overview & Compiler Configuration
This specification defines the formatting, visual identity, dynamic assets (icons/logos), cover page structure, table styling, and component architecture for Budapest University of Technology and Economics (BME) engineering assignments and technical reports in **Antigravity**.

* **Required Engine:** `lualatex` (`% !TEX program = lualatex`)
  * Required for inline Lua scripting (`luacode*`) and native UTF-8 / OpenType font handling (`Latin Modern`).
* **Document Class:** `\documentclass[12pt,a4paper]{article}`
* **Language & Localization:** Hungarian (`\usepackage[magyar]{babel}`)
  * Automatically formats section naming, date conventions, table captions (*"1. táblázat."*), TOC title (*"Tartalomjegyzék"*), and continental decimal commas in math (`-1,5`).
* **Page Geometry (`geometry` package):**
  * **Paper Size:** A4 (`210mm x 297mm`, i.e., `595.28pt x 841.89pt`)
  * **Left / Right Margins:** `2.5cm` (`70.87pt`, leaving an active text width of `16.0cm` / `453.54pt`)
  * **Top Margin:** `35mm`
  * **Bottom Margin:** `30mm`
  * **Header Height (`headheight`):** `36pt` (accommodates the `1cm` department icon and two-line course header)
* **External PDF Embedding (`pdfpages`):**
  * Used in appendices (`\includepdf[pages=-]{...}`) to attach full-page CAD assembly drawings (e.g., SolidWorks exports) and manufacturer component datasheets directly at the end of the report.

---

## 2. Dynamic Icon & Institutional Logo System (Subject & Department Dependent)

The template uses a **two-level logo architecture**:
1. **Running Header Icon (`\fancyhead[L]`):** A single department icon (`height=1cm`) displayed in the top-left header of every content page (Page 2 onwards).
2. **Cover Page Institutional Footer Strip:** A 3-column bottom bar on the Main Title Page displaying the **University Logo** (left), **Faculty Logo** (center), and **Department Icon** (right).

### 2.1. Cover Page Fixed Institutional Logos (Columns 1 & 2)
| Slot Variable | Default File | Format & Aspect | Institutional Text Beneath Logo (`\footnotesize`, centered) |
| :--- | :--- | :--- | :--- |
| `{{university_logo}}` | `bme_logo.pdf` | Vector PDF (`703x189` pt, wide) | `Budapesti Műszaki és Gazdaságtudományi Egyetem` <br> `1111 Budapest, Műegyetem rkp. 3.` |
| `{{faculty_logo}}` | `gpk_logo.png` | Square PNG (`484x484` px) | `Gépészmérnöki kar` <br> `(BME GPK)` |

### 2.2. Subject-Dependent Department Icons (Running Header & Cover Page Column 3)
Because the paper's subject changes across courses, Antigravity should dynamically map the `{{department_icon}}` and `{{department_name}}` variables based on the course code (`BMEGE...`):

| Department / Subject Area | Course Code Prefix | Icon Filename | Cover Page Column 3 Label (`{{department_name}}`) |
| :--- | :--- | :--- | :--- |
| **Mechatronics, Optics & Mechanical Engineering Informatics (MOGI)** *(Control Systems, Technical Optics, Mechatronics)* | `BMEGEMIBM...` (e.g., `BMEGEMIBMRI`, `BMEGEMIBMOA`) | `mogi.png` | `Mechatronika, Optika és` <br> `Gépészeti Informatika` <br> `Tanszék` |
| **Machine and Product Design (GT3)** *(CAD, Machine Elements, Product Design)* | `BMEGEGT...` | `gt3.png` | `Gép- és Terméktervezés` <br> `Tanszék` |
| **Applied Mechanics (MM)** *(Statics, Strength of Materials, Dynamics, Vibrations)* | `BMEGEMM...` | `mm.png` | `Műszaki Mechanika` <br> `Tanszék` |
| **Energy Engineering (ET)** *(Thermodynamics, Heat Transfer, Power Plants)* | `BMEGEET...` | `et.png` | `Energetikai Gépek és` <br> `Rendszerek Tanszék` |
| **Fluid Mechanics (ÁI)** *(Fluid Dynamics, Turbomachinery)* | `BMEGEAI...` | `ai.png` | `Áramlástan` <br> `Tanszék` |
| **Manufacturing Science and Engineering (GYT)** *(Machining, CNC, Production)* | `BMEGEGY...` | `gyt.png` | `Gyártástudomány és` <br> `-technológia Tanszék` |
| **Materials Science and Engineering (ATT)** *(Metallurgy, Polymers, Material Testing)* | `BMEGEAT...` | `att.png` | `Anyagtudomány és` <br> `-technológia Tanszék` |
| **Building Services and Process Engineering (ÉPGET)** *(HVAC, Process Engineering)* | `BMEGEVG...` | `epget.png` | `Épületgépészeti és Eljárástechnikai` <br> `Tanszék` |
| **Polymer Engineering (PT)** *(Composites, Polymer Processing)* | `BMEGEPT...` | `pt.png` | `Polimertechnika` <br> `Tanszék` |
| **General / Fallback BME GPK** | `BMEGEXX...` | `bme_gpk.png` | `Gépészmérnöki Kar` |

---

## 3. Color Palette Specification (`xcolor`)

All custom colors are defined in the RGB color space (`0–255`), supplemented by standard `xcolor` grayscale mixes for tables and diagrams.

| Color Name | LaTeX Definition | RGB Values | Hex Code | Primary Usage |
| :--- | :--- | :--- | :--- | :--- |
| **`BMEred`** | `\definecolor{BMEred}{RGB}{209, 0, 0}` | `209, 0, 0` | `#D10000` | Reference signal (`r(t)`) plots in `pgfplots`, primary warning/accent highlights. |
| **`BMEgreen`** | `\definecolor{BMEgreen}{RGB}{85, 157, 0}` | `85, 157, 0` | `#559D00` | Full-bleed `3pt` horizontal divider rule in running headers and across the Main Cover Page. |
| **`mygreen`** | `\definecolor{mygreen}{RGB}{28, 172, 0}` | `28, 172, 0` | `#1CAC00` | Code comments (`commentstyle`) inside `listings` MATLAB blocks. |
| **`mylilas`** | `\definecolor{mylilas}{RGB}{170, 55, 241}` | `170, 55, 241` | `#AA37F1` | String literals (`stringstyle`) inside `listings` MATLAB blocks. |
| **`tableGray`** | `\definecolor{tableGray}{gray}{0.95}` (`gray!5`) | `242, 242, 242` | `#F2F2F2` | Alternating row background fill in specification and data tables. |
| **`gray!10`** | Built-in `xcolor` mix | `230, 230, 230` | `#E6E6E6` | Fill color for TikZ control system blocks (`fill=gray!10`). |
| **`green!60!black`** | Built-in `xcolor` mix | `0, 153, 0` | `#009900` | Disturbance signal (`d_o(t)`) dotted curve in `pgfplots`. |
| **`blue`** | Base `xcolor` | `0, 0, 255` | `#0000FF` | Primary system output curve (`y(t)`) in `pgfplots` and MATLAB keywords (`keywordstyle`). |
| **`orange`** | Base `xcolor` | `255, 128, 0` | `#FF8000` | Error signal curve (`e(t)`) in `pgfplots`. |

---

## 4. Typography & Font Hierarchy

The document uses the **Latin Modern** (`lmodern`) font family (loaded automatically by `lualatex`):
* **Serif Body Font:** `LMRoman12-Regular` (`12pt` base size) with `LMRoman12-Bold` for headings, table headers, and key results.
* **Monospace Font:** `LMMonoLt10-Bold` (used at `24.8pt` `\Huge` for the main Cover Page title) and `LMMono12-Regular` / `\footnotesize` for code listings and URLs.
* **Math Font:** `LatinModernMath-Regular` / `CMMI`.

### Typographic Scale
| Element | LaTeX Command / Size | Font Family & Style | Alignment |
| :--- | :--- | :--- | :--- |
| **Cover Page Main Title** | `\Huge\texttt{\textbf{...}}` (`24.79pt`) | Monospace Bold (`LMMonoLt10-Bold`) | Centered |
| **Cover Page Author & Neptun** | `\LARGE\textbf{...}` (`17.22pt`) | Serif Bold (`LMRoman12-Bold`) | Centered |
| **Cover Page Course & Faculty Info** | `\large` (`14.35pt`) | Serif Regular (`LMRoman12-Regular`) | Centered |
| **Cover Page Date** | `\normalsize` (`12pt`) | Serif Regular (`LMRoman12-Regular`) | Centered |
| **Cover Page Logo Captions** | `\footnotesize` (`10pt`) | Serif Regular (`LMRoman10-Regular`) | Centered (3 columns) |
| **Header Course Title** | `\large\textbf{...}` (`14.35pt`) | Serif Bold (`LMRoman12-Bold`) | Right-aligned |
| **Header Course Code** | `\normalsize\textbf{...}` (`12pt`) | Serif Bold (`LMRoman12-Bold`) | Right-aligned |
| **Section (`\section`) & TOC Title** | `\LARGE\textbf{...}` (`17.22pt`) | Serif Bold (`LMRoman12-Bold`) | Left-aligned |
| **Subsection (`\subsection`)** | `\large\textbf{...}` (`14.35pt`) | Serif Bold (`LMRoman12-Bold`) | Left-aligned |
| **Body Prose & Table Cells** | `\normalsize` (`12pt`) | Serif Regular (`LMRoman12-Regular`) | Justified (Prose) / Left (Tables) |
| **Code Listings (`lstlisting`)** | `\ttfamily\footnotesize` (`10pt`) | Monospace Regular | Left-aligned |
| **Line Numbers (`lstlisting`)** | `\tiny\color{gray}` (`6pt`) | Serif/Mono Tiny Gray | Left margin (`numbersep=9pt`) |

* **Section Math Safety:** Always wrap mathematical expressions inside `\section` and `\subsection` titles with `\texorpdfstring{$...$}{fallback}` to prevent `hyperref` PDF bookmark warnings.

---

## 5. Main Page (Cover Page) & Table of Contents Style

For larger homework assignments and project reports (such as the Technical Optics report), the document starts with a dedicated **Main Title Page** (`\thispagestyle{empty}`) followed by a **Table of Contents** page before the numbered sections begin.

### 5.1. Cover Page Visual Layout (Top to Bottom)
1. **Page Style:** `\thispagestyle{empty}` (suppresses running header and footer on the cover page).
2. **Title Block (Upper Half):**
   * **Report Title:** Centered, `\Huge\texttt{\textbf{...}}` (Monospace Bold, `24.8pt`), spanning 1–2 lines.
   * **Vertical Spacing:** `~2.5cm` (`\vspace{2.5cm}`).
   * **Author & Neptun Code:** Centered, `\LARGE\textbf{Hallgató Neve \quad NEPTUN}` (`17.2pt` bold).
   * **Metadata Lines (`\large`, `14.35pt`, regular weight, `~0.3cm` line spacing):**
     * Line 1: `Gépészmérnöki Kar, Budapesti Műszaki és Gazdaságtudományi Egyetem`
     * Line 2: `{{course_name}} - {{course_code}}` (e.g., `Műszaki Optika - BMEGEMIBMOA`)
     * Line 3: `Tárgyfelelős: {{instructor_name}}` (e.g., `Tárgyfelelős: Dr. Nagy Balázs Vince`)
   * **Date Line:** `\vspace{0.8cm}` followed by `\normalsize {{date}}` (e.g., `2026. május 8.`).
3. **Full-Bleed Green Divider Line:**
   * Placed immediately below the date (`\vspace{0.5cm}`).
   * Spans the **entire physical paper width (`\paperwidth`)** from edge to edge in `BMEgreen` with a thickness of `3pt`:
     ```latex
     \noindent\makebox[0pt][l]{\hspace*{-\oddsidemargin}\hspace*{-1in}\color{BMEgreen}\rule{\paperwidth}{3pt}}
     ```
4. **Bottom Institutional Logo Strip (`\vfill` pushed to bottom):**
   * A 3-column layout (`\begin{minipage}[t]{0.38\textwidth}`, `\begin{minipage}[t]{0.24\textwidth}`, `\begin{minipage}[t]{0.34\textwidth}`) aligned near the bottom margin:
     * **Left Column:** University logo (`height=1.6cm`), followed by `\footnotesize` centered university name and address (`1111 Budapest, Műegyetem rkp. 3.`).
     * **Middle Column:** Faculty logo (`height=2.0cm`), followed by `\footnotesize` centered faculty name (`Gépészmérnöki kar \\ (BME GPK)`).
     * **Right Column:** Department icon (`height=1.4cm`), followed by `\footnotesize` centered department name (`Mechatronika, Optika és \\ Gépészeti Informatika \\ Tanszék`).

### 5.2. Table of Contents Page (Page 2)
* Starts on a new page (`\newpage`) with `\setcounter{page}{1}` so the TOC is numbered as `1. oldal`.
* Uses the standard running header (`mogi.png` on left, course title + `BMEgreen` `3pt` rule on right) and running footer.
* Renders `\tableofcontents` (*"Tartalomjegyzék"*), where top-level `\section` entries are bold without dot leaders and `\subsection` entries are regular weight with dotted leaders (`...`).
* Ends with `\newpage` so Section 1 starts cleanly at the top of `2. oldal`.

---

## 6. Running Header & Footer Architecture (`fancyhdr`)

Applied to all pages after the Cover Page (`\pagestyle{fancy}`):

* **Top-Left Header (`\fancyhead[L]`):**
  * Department icon (`\includegraphics[height=1cm]{mogi.png}`).
* **Top-Right Header (`\fancyhead[R]`):**
  * Right-aligned `15cm` `\parbox` containing:
    * Line 1: `\large\textbf{<Course Title>}` (e.g., *Műszaki Optika házi feladat* or *Rendszer- és irányítástechnika*)
    * Line 2: `\textbf{<Course Code>}` (e.g., *BMEGEMIBMOA* or *BMEGEMIBMRI*)
    * Bottom padding: `\vspace{0.5cm}`
* **Full-Bleed Green Header Rule (`\headrule`):**
  * Draws a `3pt` thick `BMEgreen` bar across the entire `210mm` width of the A4 page.
* **Three-Part Running Footer (`\fancyfoot`):**
  * **Left (`\fancyfoot[L]`):** Assignment Name & Date (for short papers without a cover page) or empty (when a Cover Page is used).
  * **Center (`\fancyfoot[C]`):** `\thepage. oldal` (Hungarian page numbering).
  * **Right (`\fancyfoot[R]`):** `{{author_name}} \\ {{neptun_code}}` (2 lines, right-aligned).

---

## 7. Table Formatting & Styling Specification (`colortbl` / `tabularx` / `multirow`)

Tables in the report follow a distinctive **modern borderless white-grid aesthetic** with alternating light-gray (`gray!5`) and white rows.

### 7.1. Core Visual Rules for Tables
* **Full Text-Width Span:** Tables span exactly `\textwidth` (`16cm` / `453.54pt`) using `tabularx{\textwidth}{...}`.
* **White Grid Lines (No Black Borders):**
  * All vertical and horizontal cell dividers are drawn in **solid white (`\arrayrulecolor{white}`)** with a rule thickness of **`2pt`** (`\setlength{\arrayrulewidth}{2pt}`).
  * For 2-column specification tables, the central vertical divider can be widened to `3pt` (`!{\color{white}\vrule width 3pt}`) to create a crisp visual gap between the property name column and the value column.
* **Alternating Row Fills:**
  * Uses `tableGray` (`\definecolor{tableGray}{gray}{0.95}`, i.e., `gray!5`) alternating with pure `white`.
  * **Style A — 3-Column Parameter Tables (e.g., Table 1: *Megadott adatok*):**
    * **Header Row:** Bold text (`\textbf{Megnevezés}`, `\textbf{Jelölés}`, `\textbf{Adat}`) on a `white` background.
    * **Data Rows:** Row 1 `white`, Row 2 `tableGray`, Row 3 `white`, Row 4 `tableGray`, etc. (`\rowcolors{2}{white}{tableGray}`).
    * **Column Widths:** 3 equal-width left-aligned `X` columns (`|X|X|X|`).
  * **Style B — 2-Column Technical Specification Tables (e.g., Tables 2–5: *Optikai tulajdonságok / Detektor adatai*):**
    * **Header / First Row:** Starts on `tableGray` (`\rowcolors{1}{tableGray}{white}`), with bold section/category headers in Column 1 (e.g., `\textbf{Optical Properties}`, `\textbf{Sensor}`) or multi-column bold headers (`\textbf{Model}`, `\textbf{Version}`, `\textbf{MP}`, `\textbf{Imaging Sensor}`).
    * **Multi-Row Grouping:** Uses `\multirow` for properties with multiple sub-values (e.g., *Field of View at Max Sensor Format* spanning `Horizontal: 84.7°`, `Vertical: 66.1°`, `Diagonal: 100.1°` on a white background).
* **Cell Padding:**
  * Vertical padding: `\renewcommand{\arraystretch}{1.25}` (gives `~14.45pt` row height for single-line rows).
  * Horizontal padding: `\setlength{\tabcolsep}{6pt}`.
* **Table Captions:**
  * Always placed **below** the `tabularx` environment (`\caption{...}`).
  * Automatically prefixed with `"X. táblázat."` by `babel[magyar]`, often ending with a bracketed reference citation (e.g., `\caption{A választott objektív optikai tulajdonságai \cite{ref2}}`).

### 7.2. Reference LaTeX Implementation for Both Table Styles
```latex
% Required in preamble:
% \usepackage[table]{xcolor}
% \usepackage{tabularx, multirow}
% \definecolor{tableGray}{gray}{0.95}

% --- STYLE A: 3-Column Input Parameters Table ---
\begin{table}[ht!]
\centering
\renewcommand{\arraystretch}{1.25}
\setlength{\tabcolsep}{6pt}
\setlength{\arrayrulewidth}{2pt}
\arrayrulecolor{white}
\rowcolors{2}{white}{tableGray}
\begin{tabularx}{\textwidth}{|X|X|X|}
\hline
\rowcolor{white}
\textbf{Megnevezés} & \textbf{Jelölés} & \textbf{Adat} \\ \hline
Tárgy látószöge & $\varphi$ & $2^\circ$ \\ \hline
Legkisebb méret & $x$ & $0.5\text{ mm}$ \\ \hline
Tárgytávolság & $s$ & $200\text{ mm}$ \\ \hline
Szín & & Monokróm \\ \hline
Laterális sebesség & $v$ & $0.01\text{ m/s}$ \\ \hline
Megvilágítás & & Napfény \\ \hline
\end{tabularx}
\caption{A megadott adatok TRRHBX neptun kód alapján \cite{hazi}}
\end{table}

% --- STYLE B: 2-Column Component Specification Table with Multirow ---
\begin{table}[ht!]
\centering
\renewcommand{\arraystretch}{1.25}
\setlength{\tabcolsep}{6pt}
\setlength{\arrayrulewidth}{2pt}
\arrayrulecolor{white}
\begin{tabularx}{\textwidth}{|X!{\color{white}\vrule width 3pt}X|}
\hline
\rowcolor{tableGray}
\textbf{Optical Properties} & \\ \hline
\rowcolor{white}
 & Horizontal: $84.7^\circ$ \\
\rowcolor{white}
 & Vertical: $66.1^\circ$ \\
\rowcolor{white}
\multirow{-3}{\linewidth}{Field of View at Max Sensor Format} & Diagonal: $100.1^\circ$ \\ \hline
\rowcolor{tableGray}
Focal length & $4.50\text{ mm}$ \\ \hline
\rowcolor{white}
Working distance & $25 - \infty$ \\ \hline
\rowcolor{tableGray}
Lens wavelength range & VIS \\ \hline
\end{tabularx}
\caption{A választott objektív optikai tulajdonságai \cite{lencse}}
\end{table}
```

---

## 8. Mathematical, Graphic & Code Component Styles

### 8.1. Lua Computation Bridge (`luacode*`)
* Placed in the preamble to pre-calculate exact floating-point constants and export them as TeX macros (`\def\cExpOne{...}`) via `\directlua{calculate_all()}` right after `\begin{document}`.

### 8.2. Mathematical Derivations (`amsmath`)
* **Numbered Equations (`equation`):** Used for every key derivation step so equations are sequentially numbered `(1)`, `(2)`, `(3)` down the right margin.
* **Final Results:** Highlighted inside `equation` or `align*` using `\mathbf{...}`.

### 8.3. TikZ Block Diagrams & Ray-Tracing Schematics
* **Block Style:** `rectangle, draw, thick, fill=gray!10, minimum height=3em, minimum width=4em, align=center`.
* **Summing Junctions:** `draw, circle, inner sep=0mm, minimum size=6mm, thick`.
* **Arrows:** `>=Stealth`, `thick`, `node distance=2cm`.

### 8.4. Data Plots (`pgfplots`)
* `\pgfplotsset{compat=1.18}`, `width=15cm`, `height=8cm`–`8.5cm`, `grid=both`, `axis lines=middle`, `samples=400`.
* **Curve Hierarchy:** Reference input in `BMEred, dashed, thick`; disturbance in `green!60!black, dotted, thick`; output in `blue, line width=1.5pt`; error in `orange, line width=1.5pt`.

### 8.5. Code Listings (`listings`) & Appendices (`pdfpages`)
* **MATLAB Code:** Framed (`frame=single`), `basicstyle=\ttfamily\footnotesize`, left line numbers (`\tiny\color{gray}`), `blue` keywords, `mylilas` strings, `mygreen` comments.
* **Datasheet & CAD Drawing Appendices:** Embedded at the end of the document using `\includepdf[pages=-]{filename.pdf}` from the `pdfpages` package.

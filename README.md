# 🎓 BME STEM Homework & Technical Report LaTeX Template

[![Compiler: LuaLaTeX](https://img.shields.io/badge/Compiler-LuaLaTeX-blue.svg)](https://www.luatex.org/)
[![Language: Hungarian](https://img.shields.io/badge/Language-Magyar%20(Babel)-green.svg)](https://ctan.org/pkg/babel-hungarian)
[![Institution: BME](https://img.shields.io/badge/University-BME%20Budapest-red.svg)](https://www.bme.hu)
[![Faculty: GPK](https://img.shields.io/badge/Faculty-BME%20GPK-orange.svg)](https://gpk.bme.hu)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A premier, highly standardized **LaTeX template** engineered specifically for technical reports, homework assignments (féléves házi feladatok), laboratory logs (mérési jegyzőkönyvek), and control system designs at the **Budapest University of Technology and Economics (Budapesti Műszaki és Gazdaságtudományi Egyetem – BME)**.

Pre-configured for the **Faculty of Mechanical Engineering (GPK)** and easily adaptable to other BME faculties (VIK, TTK, KJK, VBK).

---

## 📑 Table of Contents

1. [Key Features](#1-key-features)
2. [Compiler & Engine Requirements](#2-compiler--engine-requirements)
3. [Document Architecture & Page Geometry](#3-document-architecture--page-geometry)
4. [BME Institutional Identity & Dynamic Logo System](#4-bme-institutional-identity--dynamic-logo-system)
   - [4.1 Cover Page Institutional Logos (Columns 1 & 2)](#41-cover-page-institutional-logos-columns-1--2)
   - [4.2 Department Icons by Course Prefix (Column 3 & Header)](#42-department-icons-by-course-prefix-column-3--header)
5. [Cover Page & Table of Contents Specification](#5-cover-page--table-of-contents-specification)
   - [5.1 Cover Page Layout & Full-Bleed Divider](#51-cover-page-layout--full-bleed-divider)
   - [5.2 Table of Contents Page](#52-table-of-contents-page)
6. [Running Headers & Footers (`fancyhdr`)](#6-running-headers--footers-fancyhdr)
7. [Visual Design System](#7-visual-design-system)
   - [7.1 Color Palette (`xcolor`)](#71-color-palette-xcolor)
   - [7.2 Typography & Scale (Latin Modern)](#72-typography--scale-latin-modern)
8. [Engineering Table Specifications](#8-engineering-table-specifications)
   - [8.1 Design Philosophy (Borderless White-Grid)](#81-design-philosophy-borderless-white-grid)
   - [8.2 Style A: 3-Column Input Parameters](#82-style-a-3-column-input-parameters)
   - [8.3 Style B: 2-Column Technical Specifications (Multi-Row)](#83-style-b-2-column-technical-specifications-multi-row)
   - [8.4 Complete Table Reference Implementation](#84-complete-table-reference-implementation)
9. [STEM Components & Modeling Suite](#9-stem-components--modeling-suite)
   - [9.1 Lua Computation Bridge (`luacode*`)](#91-lua-computation-bridge-luacode)
   - [9.2 Mathematical Derivations (`amsmath`)](#92-mathematical-derivations-amsmath)
   - [9.3 Control System Block Diagrams (TikZ)](#93-control-system-block-diagrams-tikz)
   - [9.4 Response Curves & Bode Plots (`pgfplots`)](#94-response-curves--bode-plots-pgfplots)
   - [9.5 Source Code Listings (`listings`)](#95-source-code-listings-listings)
   - [9.6 CAD Assembly & Datasheet Appendices (`pdfpages`)](#96-cad-assembly--datasheet-appendices-pdfpages)
10. [Recommended Project Layout](#10-recommended-project-layout)
11. [Quick Start & Compilation Guide](#11-quick-start--compilation-guide)
12. [License](#12-license)

---

## 1. Key Features

- **🏛️ BME Institutional Branding:** Native support for the 3-tier BME hierarchy (University, Faculty, and Department icon dynamic mapping based on course code).
- **🇭🇺 Full Hungarian Localization:** Built on `\usepackage[magyar]{babel}` with continental decimal commas (`-1,5`), Hungarian table captions (*"1. táblázat."*), and localized pagination (*"1. oldal"*).
- **⚡ LuaLaTeX Computation Engine:** Pre-calculate system parameters, transfer functions, and exact floating-point values directly via inline Lua scripts (`luacode*`).
- **📊 Modern White-Grid Tables:** Clean, borderless tables with crisp white cell dividers and alternating light-gray fills (`tableGray`).
- **🎛️ Control Systems & STEM Ready:** Pre-styled TikZ block diagrams, `pgfplots` step/Bode responses, framed MATLAB/Python listings, and full-page CAD appendix embedding.
- **🎨 BME Corporate Identity Colors:** Official BME red (`BMEred`), corporate green (`BMEgreen`), and standardized signal plotting hues.

---

## 2. Compiler & Engine Requirements

| Property | Value / Requirement | Notes |
| :--- | :--- | :--- |
| **Compiler Engine** | **`lualatex`** | Declared via `% !TEX program = lualatex`. Required for `luacode*` and native OpenType font loading. |
| **Document Class** | `\documentclass[12pt,a4paper]{article}` | Base body size `12pt`. |
| **Language & Locale** | Hungarian (`\usepackage[magyar]{babel}`) | Handles hyphenation, TOC title (*"Tartalomjegyzék"*), and date formats. |
| **Font System** | Latin Modern (`lmodern`) | Loaded with OpenType Roman, Sans, and Math typefaces. |

---

## 3. Document Architecture & Page Geometry

Configured via the `geometry` package to balance readability and full-width engineering figures:

```latex
\usepackage[
  a4paper,
  left=2.5cm,
  right=2.5cm,
  top=35mm,
  bottom=30mm,
  headheight=36pt
]{geometry}
```

- **Paper Size:** A4 (`210mm` $\times$ `297mm`, i.e., `595.28pt` $\times$ `841.89pt`).
- **Active Text Width:** `16.0cm` (`453.54pt`).
- **Margins:** Left & Right `25mm`, Top `35mm`, Bottom `30mm`.
- **Header Height (`headheight`):** `36pt` (specifically sized to host the `1cm` department icon and the two-line course header).

---

## 4. BME Institutional Identity & Dynamic Logo System

The template features a **two-level branding architecture**:
1. **Running Header Icon (`\fancyhead[L]`):** Department icon (`height=1cm`) displayed on every content page (Page 2 onward).
2. **Cover Page Footer Strip:** A 3-column bottom bar on the title page featuring the University Logo, Faculty Logo, and Department Icon.

```
+-----------------------------------------------------------------------------+
|                                 COVER PAGE                                  |
|                                                                             |
|                         [ MAIN REPORT TITLE ]                               |
|                                                                             |
|                    Author Name    •    NEPTUN CODE                          |
|                     Course Title - Course Code                              |
|                    Tárgyfelelős: Oktató Neve                                |
|                           2026. május 8.                                    |
|                                                                             |
| ======================= FULL-BLEED BMEGREEN RULE ========================= |
|                                                                             |
|    [ BME Logo ]               [ GPK Logo ]             [ Department Icon ]  |
|  Budapesti Műszaki és       Gépészmérnöki Kar            Mechatronika,      |
| Gazdaságtudományi Egyetem       (BME GPK)             Optika és Gépészeti   |
|                                                       Informatika Tanszék   |
+-----------------------------------------------------------------------------+
```

### 4.1. Cover Page Institutional Logos (Columns 1 & 2)

| Slot | Asset File | Format | Subtitle Label (`\footnotesize`, centered) |
| :--- | :--- | :--- | :--- |
| **`{{university_logo}}`** | `bme_logo.pdf` | Vector PDF (`703x189` pt) | `Budapesti Műszaki és Gazdaságtudományi Egyetem`<br>`1111 Budapest, Műegyetem rkp. 3.` |
| **`{{faculty_logo}}`** | `gpk_logo.png` | Square PNG (`484x484` px) | `Gépészmérnöki Kar`<br>`(BME GPK)` |

### 4.2. Department Icons by Course Prefix (Column 3 & Header)

The department icon and label dynamically map based on the BME course code prefix:

| Department / Subject Area | Course Prefix | Icon File | Department Subtitle (`{{department_name}}`) |
| :--- | :--- | :--- | :--- |
| **Mechatronics, Optics & Mech. Info (MOGI)** | `BMEGEMIBM...` | `mogi.png` | `Mechatronika, Optika és`<br>`Gépészeti Informatika Tanszék` |
| **Manufacturing Science & Tech (GTT / GYT)** | `BMEGEGY...` | `gtt.png` | `Gyártástudomány és -technológia Tanszék` |
| **Materials Science & Tech (ATT)** | `BMEGEAT...` | `att.jpg` | `Anyagtudomány és -technológia Tanszék` |
| **Hydrodynamic Systems (HDR / ÁI)** | `BMEGEAI...` | `hdr.jpg` | `Hidrodinamikai Rendszerek Tanszék` |
| **Polymer Engineering (PT)** | `BMEGEPT...` | `pt.png` | `Polimertechnika Tanszék` |
| **General / Fallback GPK** | `BMEGEXX...` | `gpk_logo.png` | `Gépészmérnöki Kar` |

---

## 5. Cover Page & Table of Contents Specification

### 5.1. Cover Page Layout & Full-Bleed Divider

The cover page suppresses standard headers/footers (`\thispagestyle{empty}`):

1. **Title Block (Top Half):**
   - **Report Title:** `\Huge\texttt{\textbf{<Cím>}}` (Monospace Bold, `24.8pt`).
   - `\vspace{2.5cm}`
   - **Author & Neptun Code:** `\LARGE\textbf{Hallgató Neve \quad NEPTUN}` (`17.2pt`).
   - **Metadata (`\large`, `14.35pt`):**
     - Line 1: `Gépészmérnöki Kar, Budapesti Műszaki és Gazdaságtudományi Egyetem`
     - Line 2: `{{course_name}} - {{course_code}}`
     - Line 3: `Tárgyfelelős: {{instructor_name}}`
   - `\vspace{0.8cm}`
   - **Date:** `\normalsize {{date}}` (e.g., `2026. május 8.`).
2. **Full-Bleed BME-Green Divider:**
   - Runs across the full physical paper width (`\paperwidth`) from the absolute left to right edge in `BMEgreen` (`3pt` thick) using TikZ overlay:
     ```latex
     \noindent
     \begin{tikzpicture}[remember picture, overlay]
       \draw[BMEgreen, line width=3pt] (current page.west |- 0, 0) -- (current page.east |- 0, 0);
     \end{tikzpicture}
     ```
3. **Institutional Footer Strip (`\vfill` at bottom):**
   - 3 minipages (`0.38\textwidth`, `0.24\textwidth`, `0.34\textwidth`) hosting the three logos and institutional addresses.

### 5.2. Table of Contents Page

- Placed on Page 2 (`\newpage`) with `\setcounter{page}{1}` so content pagination starts as `1. oldal`.
- Uses the standard running header and footer.
- Renders `\tableofcontents` (*"Tartalomjegyzék"*).
- Section math protection: Wrap math in titles with `\texorpdfstring{$...$}{fallback}` to prevent PDF bookmark warnings.

---

## 6. Running Headers & Footers (`fancyhdr`)

Configured for all pages after the cover page (`\pagestyle{fancy}`):

```latex
\pagestyle{fancy}
\fancyhf{}

% --- Running Header ---
\fancyhead[L]{\includegraphics[height=1cm]{mogi.png}}
\fancyhead[R]{%
  \parbox[b]{15cm}{\raggedleft
    \large\textbf{Műszaki Optika házi feladat}\\[2pt]
    \normalsize\textbf{BMEGEMIBMOA}\vspace{0.5cm}
  }%
}
% Full-bleed 3pt green divider rule (edge-to-edge)
\renewcommand{\headrule}{%
  \nointerlineskip
  \begin{tikzpicture}[remember picture, overlay]
    \draw[BMEgreen, line width=3pt] (current page.west |- 0, 0) -- (current page.east |- 0, 0);
  \end{tikzpicture}%
}

% --- Running Footer ---
\fancyfoot[C]{\thepage. oldal}
\fancyfoot[R]{\small Minta János\\NEPTUN}
```

---

## 7. Visual Design System

### 7.1. Color Palette (`xcolor`)

| Color Name | LaTeX Definition | RGB | Hex | Primary Role |
| :--- | :--- | :--- | :--- | :--- |
| **`BMEred`** | `\definecolor{BMEred}{RGB}{209, 0, 0}` | `209, 0, 0` | `#D10000` | Reference signals ($r(t)$), critical warnings, accents |
| **`BMEgreen`** | `\definecolor{BMEgreen}{RGB}{85, 157, 0}` | `85, 157, 0` | `#559D00` | Full-bleed horizontal rules across cover and headers |
| **`mygreen`** | `\definecolor{mygreen}{RGB}{28, 172, 0}` | `28, 172, 0` | `#1CAC00` | Code comments in MATLAB / Python listings |
| **`mylilas`** | `\definecolor{mylilas}{RGB}{170, 55, 241}` | `170, 55, 241` | `#AA37F1` | String literals in code listings |
| **`tableGray`** | `\definecolor{tableGray}{gray}{0.95}` | `242, 242, 242` | `#F2F2F2` | Alternating row background in data tables |
| **`gray!10`** | Built-in `xcolor` mix | `230, 230, 230` | `#E6E6E6` | Fill background for TikZ block diagram blocks |
| **`green!60!black`** | Built-in `xcolor` mix | `0, 153, 0` | `#009900` | Disturbance input curves ($d_o(t)$) in `pgfplots` |
| **`blue`** | Base `xcolor` | `0, 0, 255` | `#0000FF` | System output response ($y(t)$), code keywords |
| **`orange`** | Base `xcolor` | `255, 128, 0` | `#FF8000` | Control error signal curve ($e(t)$) in plots |

### 7.2. Typography & Scale (Latin Modern)

| Document Element | Command & Size | Font Family | Alignment |
| :--- | :--- | :--- | :--- |
| **Cover Title** | `\Huge\texttt{\textbf{...}}` (`24.8pt`) | Monospace Bold | Centered |
| **Cover Author / Neptun** | `\LARGE\textbf{...}` (`17.2pt`) | Serif Bold | Centered |
| **Cover Course Metadata** | `\large` (`14.4pt`) | Serif Regular | Centered |
| **Cover Date** | `\normalsize` (`12.0pt`) | Serif Regular | Centered |
| **Cover Logo Captions** | `\footnotesize` (`10.0pt`) | Serif Regular | Centered (3 cols) |
| **Header Course Title** | `\large\textbf{...}` (`14.4pt`) | Serif Bold | Right |
| **Header Course Code** | `\normalsize\textbf{...}` (`12.0pt`) | Serif Bold | Right |
| **Section (`\section`)** | `\LARGE\textbf{...}` (`17.2pt`) | Serif Bold | Left |
| **Subsection (`\subsection`)**| `\large\textbf{...}` (`14.4pt`) | Serif Bold | Left |
| **Body Prose / Tables** | `\normalsize` (`12.0pt`) | Serif Regular | Justified / Left |
| **Code Listings** | `\ttfamily\footnotesize` (`10.0pt`) | Monospace Regular | Left |
| **Line Numbers** | `\tiny\color{gray}` (`6.0pt`) | Monospace / Serif | Left margin |

---

## 8. Engineering Table Specifications

### 8.1. Design Philosophy (Borderless White-Grid)
- **Full Width:** Tables span exactly `\textwidth` (`16.0cm`) via `tabularx`.
- **Solid White Dividers:** All borders are drawn in pure white (`\arrayrulecolor{white}`) with a width of `2pt` (`\setlength{\arrayrulewidth}{2pt}`) to eliminate harsh black grids.
- **Alternating Fills:** Alternates between pure `white` and `tableGray` (`gray!5`).
- **Comfortable Padding:** `\renewcommand{\arraystretch}{1.25}` and `\setlength{\tabcolsep}{6pt}`.
- **Captions:** Placed **below** the table, auto-formatted by Babel Magyar as `"X. táblázat."`.

### 8.2. Style A: 3-Column Input Parameters
- **Use Case:** Problem inputs, given data sets, student parameter assignments.
- **Header:** Bold on white background.
- **Data Rows:** Alternating `white` and `tableGray` (`\rowcolors{2}{white}{tableGray}`).
- **Columns:** 3 equal-width `X` columns (`|X|X|X|`).

### 8.3. Style B: 2-Column Technical Specifications (Multi-Row)
- **Use Case:** Component datasheets, optical sensor specifications, motor parameters.
- **Divider:** Reinforced `3pt` vertical white separator (`!{\color{white}\vrule width 3pt}`).
- **Grouping:** Uses `\multirow` to bundle sub-attributes (e.g. horizontal, vertical, diagonal FOV).

### 8.4. Complete Table Reference Implementation

```latex
% Preamble requirements:
% \usepackage[table]{xcolor}
% \usepackage{tabularx, multirow}
% \definecolor{tableGray}{gray}{0.95}

% --- STYLE A: 3-Column Given Parameters Table ---
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
Tárgy látószöge     & $\varphi$        & $2^\circ$     \\ \hline
Legkisebb méret     & $x$              & $0{,}5\text{ mm}$ \\ \hline
Tárgytávolság       & $s$              & $200\text{ mm}$   \\ \hline
Laterális sebesség  & $v$              & $0{,}01\text{ m/s}$ \\ \hline
\end{tabularx}
\caption{A megadott feladatparaméterek a NEPTUN Neptun-kód alapján \cite{hazi}}
\end{table}

% --- STYLE B: 2-Column Component Specification with Multirow ---
\begin{table}[ht!]
\centering
\renewcommand{\arraystretch}{1.25}
\setlength{\tabcolsep}{6pt}
\setlength{\arrayrulewidth}{2pt}
\arrayrulecolor{white}
\begin{tabularx}{\textwidth}{|X!{\color{white}\vrule width 3pt}X|}
\hline
\rowcolor{tableGray}
\textbf{Optikai tulajdonság} & \textbf{Érték / Specifikáció} \\ \hline
\rowcolor{white}
 & Vízszintes: $84{,}7^\circ$ \\
\rowcolor{white}
 & Függőleges: $66{,}1^\circ$ \\
\rowcolor{white}
\multirow{-3}{\linewidth}{Látómező (FOV)} & Diagonális: $100{,}1^\circ$ \\ \hline
\rowcolor{tableGray}
Gyújtótávolság ($f$) & $4{,}50\text{ mm}$ \\ \hline
\rowcolor{white}
Munkatávolság        & $25\text{ mm} - \infty$ \\ \hline
\end{tabularx}
\caption{A választott ipari kameraoptika műszaki adatai \cite{adatlap}}
\end{table}
```

---

## 9. STEM Components & Modeling Suite

### 9.1. Lua Computation Bridge (`luacode*`)
Embed inline Lua functions directly in the preamble or before sections to calculate numeric parameters automatically:

```latex
\usepackage{luacode}
\begin{luacode*}
function calculate_system()
    local R = 120.0
    local C = 4.7e-6
    local tau = R * C
    tex.print(string.format("\\def\\tauVal{%.4f}", tau))
end
\end{luacode*}
\directlua{calculate_system()}
% The computed value is now accessible in LaTeX via \tauVal
```

### 9.2. Mathematical Derivations (`amsmath`)
- Always use numbered equations (`\begin{equation} ... \end{equation}`) for key analytical steps.
- Highlight definitive transfer functions and final numerical results with `\mathbf{...}`.
- Use Hungarian decimal commas: `$s = -1{,}5$` (or `siunitx` with `output-decimal-marker={,}`).

### 9.3. Control System Block Diagrams (TikZ)
Standardized styles for control loops:

```latex
\usepackage{tikz}
\usetikzlibrary{shapes,arrows.meta,positioning}

\tikzset{
    block/.style={rectangle, draw, thick, fill=gray!10, minimum height=3em, minimum width=4em, align=center},
    sum/.style={draw, circle, inner sep=0mm, minimum size=6mm, thick},
    input/.style={coordinate},
    output/.style={coordinate},
    >=Stealth
}
```

### 9.4. Response Curves & Bode Plots (`pgfplots`)
- Pre-configured with `\pgfplotsset{compat=1.18}`, `width=15cm`, `height=8.5cm`, `grid=both`.
- Standard signal traces:
  - Reference signal ($r(t)$): `BMEred, dashed, thick`
  - Disturbance ($d(t)$): `green!60!black, dotted, thick`
  - System output ($y(t)$): `blue, line width=1.5pt`
  - Error signal ($e(t)$): `orange, line width=1.5pt`

### 9.5. Source Code Listings (`listings` & MATLAB Dark Theme)
The template includes an authentic **MATLAB Editor Dark Theme** palette:

```latex
\definecolor{matlabDarkBg}{RGB}{24, 24, 24}       % Editor background (#181818)
\definecolor{matlabFg}{RGB}{240, 240, 240}       % Plain text / identifiers (#F0F0F0)
\definecolor{matlabComment}{RGB}{148, 239, 132}   % Comment lime green (#94EF84)
\definecolor{matlabKeyword}{RGB}{214, 148, 255}   % Builtin & keyword purple (#D694FF)
\definecolor{matlabString}{RGB}{245, 175, 115}    % String peach/orange (#F5AF73)
\definecolor{matlabNumber}{RGB}{136, 136, 136}    % Gutter line numbers (#888888)
\definecolor{matlabBorder}{RGB}{45, 45, 45}       % Subtle container border (#2D2D2D)

\lstdefinestyle{matlabdark}{
  language=Matlab,
  backgroundcolor=\color{matlabDarkBg},
  basicstyle=\ttfamily\footnotesize\color{matlabFg},
  keywordstyle=\color{matlabKeyword}\bfseries,
  commentstyle=\color{matlabComment},
  stringstyle=\color{matlabString},
  numbers=left,
  numberstyle=\tiny\color{matlabNumber},
  numbersep=10pt,
  frame=single,
  rulecolor=\color{matlabBorder},
  frameround=tttt,
  breaklines=true,
  showstringspaces=false,
  tabsize=4,
  captionpos=b,
  morekeywords={clear, clc, close, syms, all, tf, feedback, step, figure, grid, title, xlabel, ylabel}
}
\lstset{style=matlabdark}
```

### 9.6. CAD Assembly & Datasheet Appendices (`pdfpages`)
Attach full-page SolidWorks / Inventor 2D manufacturing drawings and manufacturer component datasheets seamlessly at the end of the report:

```latex
\usepackage{pdfpages}
\appendix
\section{Mellékletek: Összeállítási rajzok és gyári adatlapok}
\includepdf[pages=-, scale=0.95, pagecommand={\thispagestyle{fancy}}]{melleklet_osszeallitas.pdf}
```

---

## 10. Recommended Project Layout

```text
stem-homework-template-latex/
├── main.tex                 # Master LaTeX document
├── preamble.tex             # Packages, TikZ/pgfplots styles, colors, listings
├── metadata.tex             # BME course code, title, student & instructor data
├── assets/                  # Logos and department icons
│   ├── bme_logo.pdf         # BME University logo
│   ├── gpk_logo.png         # BME Faculty logo (GPK/VIK)
│   └── mogi.png             # Department icon (MOGI/GT3/MM/etc.)
├── figures/                 # Plots, TikZ diagrams, experimental setups
├── tasks/                   # Modular task files
│   ├── 01_feladat.tex
│   ├── 02_feladat.tex
│   └── 03_feladat.tex
├── appendices/              # Full-page CAD exports and PDF datasheets
│   └── cad_assembly.pdf
├── references.bib           # BibLaTeX bibliography database
└── README.md
```

---

## 11. Quick Start & Compilation Guide

### Local Compilation (CLI / latexmk)
Compile using `lualatex` with `-shell-escape` enabled (required for `luacode*` and code formatting):

```bash
# Using latexmk (recommended)
latexmk -lualatex -shell-escape main.tex

# Or manual step-by-step compilation:
lualatex -shell-escape main.tex
biber main
lualatex -shell-escape main.tex
```

### Overleaf Configuration
1. Upload this repository as a `.zip` to **Overleaf**.
2. Open **Menu** (top-left corner).
3. Set **Compiler** to **`LuaLaTeX`**.
4. Set **TeX Live Version** to latest (`2024` or `2025`).
5. Recompile!

---

## 12. License

Distributed under the **MIT License**. Created for the students and researchers of **Budapest University of Technology and Economics (BME)**.

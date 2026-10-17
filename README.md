# 🎓 BME STEM LaTeX Template & Component Library

[![Compiler: LuaLaTeX](https://img.shields.io/badge/Compiler-LuaLaTeX-blue.svg)](https://www.luatex.org/)
[![Language: Hungarian](https://img.shields.io/badge/Language-Magyar%20(Babel)-green.svg)](https://ctan.org/pkg/babel-hungarian)
[![Institution: BME](https://img.shields.io/badge/University-BME%20Budapest-red.svg)](https://www.bme.hu)
[![Faculty: GPK](https://img.shields.io/badge/Faculty-BME%20GPK-orange.svg)](https://gpk.bme.hu)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A standardized LaTeX template designed for homework assignments, laboratory reports (*mérési jegyzőkönyvek*), and technical projects at **Budapest University of Technology and Economics (BME)**.

- **Compiler:** `lualatex` (with `-shell-escape` for inline Lua and listings)
- **Language:** Hungarian (`\usepackage[magyar]{babel}` with continental decimal commas)
- **Compilation:**
  ```bash
  lualatex -shell-escape main.tex
  bibtex main
  lualatex -shell-escape main.tex
  ```

---

## 📚 Component Library (Copy & Paste)

- [1. Metadata & Student Info](#1-metadata--student-info)
- [2. Cover Page & Header Divider](#2-cover-page--header-divider)
- [3. Problem & Solution Boxes](#3-problem--solution-boxes)
- [4. Tables](#4-tables)
  - [4.1 Style A: 3-Column Given Parameters](#41-style-a-3-column-given-parameters)
  - [4.2 Style B: 2-Column Technical Specification (Multi-row)](#42-style-b-2-column-technical-specification-multi-row)
  - [4.3 Style C: Measurement Data Table with Units (`siunitx`)](#43-style-c-measurement-data-table-with-units-siunitx)
- [5. Code Listings (MATLAB Dark Theme)](#5-code-listings-matlab-dark-theme)
- [6. Control Systems & Block Diagrams (TikZ)](#6-control-systems--block-diagrams-tikz)
- [7. Simulation Plots & Step Responses (`pgfplots`)](#7-simulation-plots--step-responses-pgfplots)
- [8. Mathematical Equations & State-Space Models](#8-mathematical-equations--state-space-models)
- [9. Inline Lua Computation Bridge](#9-inline-lua-computation-bridge)
- [10. External PDF & CAD Appendices](#10-external-pdf--cad-appendices)

---

### 1. Metadata & Student Info

Place this in `metadata.tex` to configure your submission:

```latex
% --- Student Information ---
\newcommand{\StudentName}{Minta János}
\newcommand{\NeptunCode}{NEPTUN}
\newcommand{\StudentEmail}{minta.janos@edu.bme.hu}
\newcommand{\DegreeProgram}{Mechatronikai mérnöki MSc}

% --- Institution & Faculty ---
\newcommand{\UniversityName}{Budapesti Műszaki és Gazdaságtudományi Egyetem}
\newcommand{\UniversityAddress}{1111 Budapest, Műegyetem rkp. 3.}
\newcommand{\FacultyName}{Gépészmérnöki Kar}
\newcommand{\FacultyShort}{BME GPK}
\newcommand{\DepartmentName}{Mechatronika, Optika és\\Gépészeti Informatika Tanszék}

% --- Course Details ---
\newcommand{\CourseName}{Műszaki Optika és Szabályozástechnika}
\newcommand{\CourseCode}{BMEGEMIBMOA}
\newcommand{\InstructorName}{Dr. Oktató Neve}
\newcommand{\AssignmentTitle}{1. Házi Feladat: Szabályozási Kör Tervezése}
\newcommand{\DocumentDate}{\today}

% --- Logos (assets/ folder) ---
% Department options: mogi.png, gtt.png, att.jpg, hdr.jpg, pt.png
\newcommand{\UniversityLogoPath}{assets/bmelogo.pdf}
\newcommand{\FacultyLogoPath}{assets/gpk_logo.png}
\newcommand{\DepartmentIconPath}{assets/mogi.png}
```

---

### 2. Cover Page & Header Divider

Full-bleed edge-to-edge `BMEgreen` horizontal divider using TikZ page overlay:

```latex
% Edge-to-edge dividing rule (place between metadata and logo strip)
\vspace{0.4cm}
{\par\noindent\begin{tikzpicture}[remember picture, overlay]
  \draw[BMEgreen, line width=3pt] (current page.west |- 0, 0) -- (current page.east |- 0, 0);
\end{tikzpicture}\par}
\vspace{0.4cm}
```

3-column institutional logo footer:

```latex
\vfill
\begin{minipage}[t]{0.38\textwidth}
  \centering
  \includegraphics[height=1.5cm]{\UniversityLogoPath}\\[6pt]
  {\footnotesize \textbf{\UniversityName}\\[2pt]\UniversityAddress\par}
\end{minipage}%
\hfill
\begin{minipage}[t]{0.24\textwidth}
  \centering
  \includegraphics[height=1.8cm]{\FacultyLogoPath}\\[6pt]
  {\footnotesize \textbf{\FacultyName}\\[2pt](\FacultyShort)\par}
\end{minipage}%
\hfill
\begin{minipage}[t]{0.34\textwidth}
  \centering
  \includegraphics[height=1.4cm]{\DepartmentIconPath}\\[6pt]
  {\footnotesize \textbf{\DepartmentName}\par}
\end{minipage}
```

Running header with vertically centered department logo:

```latex
\pagestyle{fancy}
\fancyhf{}

% Logo vertically centered between the green rule and top of the page
\fancyhead[L]{%
  \ifx\DepartmentIconPath\empty\else
    \raisebox{2.25mm}{\includegraphics[height=1.1cm]{\DepartmentIconPath}}%
  \fi
}
\fancyhead[R]{%
  \parbox[b]{15cm}{\raggedleft
    \large\textbf{\CourseName}\\[2pt]
    \normalsize\textbf{\CourseCode}\vspace{0.25cm}
  }%
}

% Full-bleed edge-to-edge dividing rule
\renewcommand{\headrule}{%
  \nointerlineskip
  \begin{tikzpicture}[remember picture, overlay]
    \draw[BMEgreen, line width=3pt] (current page.west |- 0, 0) -- (current page.east |- 0, 0);
  \end{tikzpicture}%
}
\fancyfoot[C]{\thepage. oldal}
\fancyfoot[R]{\small\StudentName\\\NeptunCode}
```

---

### 3. Problem & Solution Boxes

Highlighted problem box with optional points badge and red-accented solution block:

```latex
\begin{problem}[15 pont]
Adja meg az elektromechanikai hajtás állapotegyenleteit, és számítsa ki a vágási frekvenciát a megadott paraméterek alapján!
\end{problem}

\begin{solution}
A mechanikai alrendszer Lagrange-egyenlete:
\begin{equation}
  J \ddot{\theta}(t) + b \dot{\theta}(t) + k \theta(t) = M(t)
\end{equation}
A Laplace-transzformált egyenletből az átviteli függvény:
\begin{equation}
  W(s) = \frac{\Theta(s)}{M(s)} = \frac{1}{J s^2 + b s + k}
\end{equation}
\end{solution}
```

---

### 4. Tables

#### 4.1 Style A: 3-Column Given Parameters
White grid lines on alternating white and light-gray (`tableGray`) rows:

```latex
\begin{table}[ht!]
\centering
\renewcommand{\arraystretch}{1.25}
\setlength{\tabcolsep}{8pt}
\setlength{\arrayrulewidth}{2pt}
\arrayrulecolor{white}
\rowcolors{2}{white}{tableGray}
\begin{tabularx}{\textwidth}{|X|X|X|}
\hline
\rowcolor{white}
\textbf{Megnevezés} & \textbf{Jelölés} & \textbf{Adat} \\ \hline
Tárgy látószöge               & $\varphi$        & $2^\circ$ \\ \hline
Legkisebb detektálandó méret  & $x_{\min}$       & $0{,}50\text{ mm}$ \\ \hline
Tárgytávolság                 & $s$              & $200\text{ mm}$ \\ \hline
Laterális mozgási sebesség    & $v$              & $0{,}01\text{ m/s}$ \\ \hline
Tápfeszültség                 & $U_t$            & $24\text{ V DC}$ \\ \hline
\end{tabularx}
\caption{A megadott bemeneti feladatparaméterek \cite{hazi}}
\label{tab:parameterek}
\end{table}
```

#### 4.2 Style B: 2-Column Technical Specification (Multi-row)
For component datasheets with a reinforced `3pt` central white divider:

```latex
\begin{table}[ht!]
\centering
\renewcommand{\arraystretch}{1.25}
\setlength{\tabcolsep}{8pt}
\setlength{\arrayrulewidth}{2pt}
\arrayrulecolor{white}
\begin{tabularx}{\textwidth}{|X!{\color{white}\vrule width 3pt}X|}
\hline
\rowcolor{tableGray}
\textbf{Optikai és Szenzor Paraméter} & \textbf{Specifikált Érték / Típus} \\
\noalign{\global\arrayrulewidth=2.5pt}
\arrayrulecolor{BMEgreen}\hline
\noalign{\global\arrayrulewidth=2pt}
\arrayrulecolor{white}
\rowcolor{white}
Képérzékelő típusa & Sony IMX477 CMOS (Type 1/2.3) \\ \hline
\rowcolor{tableGray}
Aktív felbontás & $4056 \times 3040\text{ (12{,}3 MP)}$ \\ \hline
\rowcolor{white}
 & Vízszintes: $84{,}7^\circ$ \\
\rowcolor{white}
 & Függőleges: $66{,}1^\circ$ \\
\rowcolor{white}
\multirow{-3}{\linewidth}{Látómező (FOV a szenzorméretre)} & Diagonális: $100{,}1^\circ$ \\ \hline
\rowcolor{tableGray}
Objektív gyújtótávolsága ($f$) & $4{,}50\text{ mm}$ (Fix fókuszú) \\ \hline
\rowcolor{white}
Tárgytávolsági tartomány ($s$) & $25\text{ mm} - \infty$ \\ \hline
\rowcolor{tableGray}
Optikai szűrő hullámhossza & $400 - 700\text{ nm}$ (VIS tartomány) \\ \hline
\end{tabularx}
\caption{A választott optikai modul műszaki specifikációi \cite{adatlap}}
\label{tab:muszaki_adatok}
\end{table}
```

#### 4.3 Style C: Measurement Data Table with Units (`siunitx`)

```latex
\begin{table}[ht!]
\centering
\begin{tabular}{r S[table-format=2.2] S[table-format=3.1] S[table-format=1.3]}
\toprule
\textbf{Mérés \#} & {\textbf{Feszültség} [\unit{\volt}]} & {\textbf{Fordulatszám} [\unit{\per\minute}]} & {\textbf{Nyomaték} [\unit{\newton\meter}]} \\
\midrule
1 & 5.00  & 450.0  & 0.120 \\
2 & 10.00 & 920.5  & 0.245 \\
3 & 15.00 & 1390.0 & 0.360 \\
4 & 20.00 & 1855.2 & 0.485 \\
5 & 24.00 & 2210.0 & 0.580 \\
\bottomrule
\end{tabular}
\caption{Mérési eredmények statikus terhelés mellett}
\label{tab:meres}
\end{table}
```

---

### 5. Code Listings (MATLAB Dark Theme)

Renders MATLAB code replicating the MATLAB editor dark theme:
- **Editor background**: `rgba(18, 18, 18)` (`#121212`)
- **Gutter background (behind line numbers)**: `rgba(33, 33, 33)` (`#212121`)
- **Vertical gutter divider line**: `rgba(125, 125, 125)` (`#7D7D7D`), 1.5pt rule separating line numbers and code text
- **Section divider lines (`\matlabrule`)**: `rgba(125, 125, 125)` (`#7D7D7D`), 1.5pt thick rule placed above `%%` section headers
- **Syntax highlighting**: Lime-green comments (`#94EF84`), purple keywords (`#D694FF`), peach strings (`#F5AF73`), and muted gray line numbers (`#888888`)

```latex
\begin{matlabbox}
\begin{lstlisting}[style=matlabdark]
% Szabalyozastechnika - 2. szorgalmi feladat
% Hallgato: Minta Janos (NEPTUN)

clear; clc; close all;

(*@\matlabrule@*)%% === 1. RÉSZ: Rendszerelemek definíciója ===

% Szimbolikus valtozok
syms s t Y_sym

% Szakasz es szabalyozo
W_p = 1 / (1 + 2*s);
W_c = 4 + 5/s;
W_v = 3;

% Bemeneti alapjel
R   = 3/s;

(*@\matlabrule@*)%% === 2. RÉSZ: Dinamikai szimuláció ===
s_num = tf('s');
P = 1 / (1 + 2*s_num);
C = 4 + 5/s_num;

L = C * P;              % Felnyitott kor
T = feedback(L, W_v);   % Zart szabalyozasi kor

figure('Name', 'Lepesvalasz');
step(T, 10);
grid on;
title('BME MOGI - Zart kor lepesvalasza');
xlabel('Ido [s]'); ylabel('Kimenet y(t)');
\end{lstlisting}
\end{matlabbox}
\captionof{lstlisting}{Irányítástechnikai szimuláció és zárt köri átviteli függvények (MATLAB)}
```

---

### 6. Control Systems & Block Diagrams (TikZ)

Negative feedback control loop featuring reference input, summing junction, controller, plant, sensor, and disturbance:

```latex
\begin{figure}[ht!]
\centering
\begin{tikzpicture}[auto, node distance=2.2cm]
  % Nodes
  \node [input, name=input] {};
  \node [sum, right=1.2cm of input] (sum1) {};
  \node [block, right=1.5cm of sum1] (controller) {$C(s)$\\PID Szabályozó};
  \node [sum, right=1.5cm of controller] (sum2) {};
  \node [block, right=1.5cm of sum2] (plant) {$P(s)$\\Szakasz};
  \node [output, right=2.0cm of plant] (output) {};
  \node [input, above=1.5cm of sum2] (disturbance) {};
  \node [block, below=1.2cm of controller] (sensor) {$H(s)$\\Visszacsatolás};

  % Signal lines
  \draw [->, thick] (input) -- node [pos=0.2] {$r(t)$} node [very near end] {$+$} (sum1);
  \draw [->, thick] (sum1) -- node {$e(t)$} (controller);
  \draw [->, thick] (controller) -- node [very near end] {$+$} (sum2);
  \draw [->, thick] (disturbance) -- node [pos=0.2] {$d(t)$} node [very near end] {$+$} (sum2);
  \draw [->, thick] (sum2) -- node {$u(t)$} (plant);
  \draw [->, thick] (plant) -- node [name=y, pos=0.7] {$y(t)$} (output);
  
  % Feedback path
  \draw [->, thick] (y) |- (sensor);
  \draw [->, thick] (sensor) -| node [very near end] {$-$} (sum1);
\end{tikzpicture}
\caption{A zárt szabályozási kör hatásvázlata}
\label{fig:szabalyozasi_kor}
\end{figure}
```

---

### 7. Simulation Plots & Step Responses (`pgfplots`)

Time-domain dynamic responses styled in official BME colors (Reference in `BMEred`, Output in `blue`, Error in `orange`, Disturbance in `green!60!black`):

```latex
\begin{figure}[ht!]
\centering
\begin{tikzpicture}
\begin{axis}[
    width=15cm,
    height=8.5cm,
    grid=both,
    grid style={line width=.1pt, draw=gray!20},
    major grid style={line width=.2pt, draw=gray!40},
    axis lines=middle,
    xlabel={$t\ [\text{s}]$},
    ylabel={Jel amplitúdó},
    xmin=0, xmax=10,
    ymin=-0.2, ymax=1.5,
    legend pos=north east,
    legend style={font=\footnotesize, fill=white, fill opacity=0.9},
    samples=300
]

% Reference input r(t)
\addplot[domain=0:10, color=BMEred, dashed, line width=1.2pt] {1.0};
\addlegendentry{Alapjel $r(t)$}

% System output y(t)
\addplot[domain=0:10, color=blue, line width=1.5pt] {
  1.0 - exp(-1.2*x)*(cos(deg(3.14*x)) + 0.38*sin(deg(3.14*x))) + 
  (x > 5 ? 0.25*exp(-1.5*(x-5))*sin(deg(4.0*(x-5))) : 0)
};
\addlegendentry{Kimenet $y(t)$}

% Error signal e(t)
\addplot[domain=0:10, color=orange, line width=1.2pt] {
  exp(-1.2*x)*(cos(deg(3.14*x)) + 0.38*sin(deg(3.14*x))) -
  (x > 5 ? 0.25*exp(-1.5*(x-5))*sin(deg(4.0*(x-5))) : 0)
};
\addlegendentry{Hibajel $e(t)$}

% Disturbance decay d(t)
\addplot[domain=5:10, color=green!60!black, dotted, line width=1.4pt] {
  0.25*exp(-1.5*(x-5))
};
\addlegendentry{Zavaráslecsengés $d_o(t)$}

\end{axis}
\end{tikzpicture}
\caption{A szabályozási kör időtartományi válaszfüggvényei}
\label{fig:lepesvalasz_plot}
\end{figure}
```

---

### 8. Mathematical Equations & State-Space Models

Numbered equations, highlighted results, and state-space matrix representations:

```latex
% Numbered analytical derivation
\begin{equation}
  \mathbf{P(s) = \frac{Y(s)}{U(s)} = \frac{K}{T_0^2 s^2 + 2\zeta T_0 s + 1}}
  \label{eq:atviteli_fuggveny}
\end{equation}

% State-space representation
\begin{align}
  \begin{bmatrix} \dot{x}_1 \\ \dot{x}_2 \end{bmatrix} &=
  \begin{bmatrix} 0 & 1 \\ -\frac{k}{J} & -\frac{b}{J} \end{bmatrix}
  \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} +
  \begin{bmatrix} 0 \\ \frac{K_t}{J} \end{bmatrix} u(t) \label{eq:allapot_matrix} \\[6pt]
  y(t) &= \begin{bmatrix} 1 & 0 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}
\end{align}
```

---

### 9. Inline Lua Computation Bridge

Pre-calculate exact numeric values via Lua and print them straight into TeX macros:

```latex
\begin{luacode*}
function calculate_design_params()
    local s_dist = 200.0   -- mm
    local phi_deg = 2.0    -- fok
    local phi_rad = phi_deg * math.pi / 180.0
    local f_target = s_dist * math.tan(phi_rad / 2.0)
    tex.print(string.format("\\def\\calcFocLength{%.2f}", f_target))
end
\end{luacode*}
\directlua{calculate_design_params()}

% Use the calculated value anywhere in text or math:
A számított elméleti gyújtótávolság: $f = \calcFocLength\text{ mm}$.
```

---

### 10. External PDF & CAD Appendices

Seamlessly attach multi-page CAD drawings, datasheets, or schematics at the end of the report while maintaining headers:

```latex
\newpage
\appendix
\section{Mellékletek: Gépészeti CAD Összeállítási Rajzok}
\label{sec:melleklet}

A tervezett modul gyártási rajzát az alábbi csatolt PDF tartalmazza:

\includepdf[
  pages=-,
  scale=0.92,
  pagecommand={\thispagestyle{fancy}}
]{appendices/cad_assembly.pdf}
```

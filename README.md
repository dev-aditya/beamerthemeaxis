# Axis — a Beamer theme for physics talks

A lab monograph, typeset on the frequency axis.

`beamerthemeaxis` restyles Beamer as an editorial lab notebook:
warm paper, near-black ink, hairline rules, and a single accent
color. The chrome is physics-native — the footline is an NMR
frequency axis with part-boundary ticks and a progress dot; part
dividers carry real pulse waveforms (GRAPE steps, a chirp, a
Ramsey pair, an echo train; the backup divider carries a stick
spectrum); bullets are spectral sticks; citations are quiet
margin annotations.


## Features

- **Paper / ink / hairline palette** — `paper #FBFAF6`, `ink #16181D`,
  `hair #9AA0A8`, one blue accent `#1D4ED8` (orange/green/red kept
  for semantic use: warnings, examples, alerts)
- **Frequency-axis footline** — hairline with end ticks, part
  boundaries at configurable fractions, Roman-numeral part labels
  I–IV, a blue progress dot, and `n/N` frame counter
- **Pulse-waveform part dividers** — oversized ghost numerals with
  real waveforms: GRAPE amplitude steps, chirp, Ramsey pair, echo
  train, stick spectrum
- **Spectral-stick bullets** — thin tikz sticks as markers,
  `\smash`'d so they never inflate line spacing
- **Flat tinted block cards** — no Beamer title bars
- **Editorial title page** — flush-left display title, short accent
  rule, small-caps kicker, optional advisor/committee lines, a chirp
  along the bottom, optional logo
- **Quiet credits** — `\credit{...}` for citations as margin
  annotations

## Requirements

- `beamer`, `tikz` (both standard TeX Live / MiKTeX)
- Designed and tested for `\documentclass[aspectratio=169,11pt]{beamer}`
- Latin Modern recommended (`\usepackage{lmodern}`) — the theme
  sets no fonts of its own, so math and text stay in one voice

## Install

Drop `beamerthemeaxis.sty` next to your `.tex` file, or install it
in your local `texmf` tree
(`~/texmf/tex/latex/beamerthemeaxis/`), or point `TEXINPUTS` at this
directory.

## Quick start

```latex
\documentclass[aspectratio=169,11pt]{beamer}
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{lmodern}

\usetheme{axis}

% --- all optional ---
\title{Two-Line Display Title\\ with a Manual Break}
\subtitle{Seminar Talk}                  % small-caps kicker
\author{A.\ Author}
\date{October 2026}
\institute{Department of Chemistry \quad$\cdot$\quad University of Somewhere}
\axisextrainfo{Seminar Series}             % repeatable: each call adds a line
\axisextrainfo{slides: example.org/axis}  % any extra info: event, advisor, URL, ...
\axislogo{logo.png}                      % bottom-right, optional
\axisset{fa=0.25, fb=0.50, fc=0.75, total=0}

\begin{document}
\begin{frame}[plain]
  \titlepage
\end{frame}

\partdivider{Introduction}{Why this matters}

\begin{frame}{A Frame}
  \begin{itemize}
    \item Spectral-stick bullets.
      \begin{itemize}
        \item Orange at the second level.
      \end{itemize}
  \end{itemize}
  \begin{block}{A block}
    Flat tinted card.
  \end{block}
  \credit{Author, Journal \textbf{1}, 123 (2025).}
\end{frame}

\backupdivider{Backup}{Anticipated questions}
\begin{frame}{B1}
  Backup slides keep the footline.
\end{frame}
\end{document}
```

Compile with `pdflatex` (three passes). `demo.tex` in this
repository exercises every feature; `demo.pdf` is its output.

## Reference

### Options — `\axisset{...}`

| Key | Default | Meaning |
|---|---|---|
| `fa`, `fb`, `fc` | `0.25`, `0.50`, `0.75` | fraction of the axis where part I/II/III ends (set to last-frame-of-part ÷ total once the deck is final) |
| `total` | `0` | frame count the progress dot saturates at; `0` = use Beamer's `\inserttotalframenumber` |

### Title-page macros

| Macro | Effect |
|---|---|
| `\axisadvisor{...}` | small gray line under the author (optional) |
| `\axiscommittee{...}` | second small gray line (optional) |
| `\axislogo{path}` | logo, bottom-right, paper-masked (optional) |

The title page also uses the standard `\title` (manual `\\` breaks
allowed), `\subtitle`, `\author`, `\date`.

### Divider macros

| Macro | Effect |
|---|---|
| `\partdivider{Title}{Subtitle}` | auto-numbered 01, 02, ...; waveform cycles GRAPE → chirp → Ramsey → echo → spectrum |
| `\backupdivider{Title}{Subtitle}` | ghost "B" + stick spectrum |
| `\axisdividerpage{Num}{Title}{Sub}{wave}` | fully manual divider |

Dividers are `[plain]` frames: no footline, no frame count.

### Waveform macros

`\wavegrape`, `\wavechirp`, `\waveramsey`, `\waveecho`,
`\wavespectrum` — usable anywhere, 13.3 cm wide on a hairline
baseline (sized for 16:9 with default margins).

### Other macros

| Macro | Effect |
|---|---|
| `\credit{text}` | quiet gray annotation line (starts its own paragraph) |

## Customization

All colors are plain `\definecolor`s — override any of them after
`\usetheme{axis}`:

```latex
\usetheme{axis}
\definecolor{axisblue}{HTML}{7C2D12}   % re-accent, e.g. rust
```

Palette names: `paper`, `ink`, `hair`, `axisblue`, `axisorange`,
`axisgreen`, `axisred`, `axisgray`.

## Notes

- Dividers and the title page are `[plain]`: the frequency axis
  appears on content frames only.
- On dense frames, Beamer's `[shrink=N]` works as usual (it scales
  fonts, not figures).

## License

LPPL 1.3c — [LaTeX Project Public License](https://www.latex-project.org/lppl/lppl-1-3c.txt). See `LICENSE`. Modified versions must be renamed or clearly marked as changed; the Current Maintainer is Aditya Dev.

## Author

Aditya Dev — Weizmann Institute of Science.
Theme built for a PhD-proposal talk on scalable and robust quantum
optimal control; the waveforms are the talk's own subject matter.

### Figure columns
When a `columns` frame puts text in one column and a figure in the other, `[T]`
clamps the figure to the column top — a figure shorter than its text partner
floats high with a void below. Either use `[c]` (beamer centers each column
against the tallest) or pad the figure column with a measured `\vspace*{...}`.
The theme's block templates are top-alignment-safe under `[T]` (verified by
probe: block / alertblock / exampleblock all start at the same y).

# STK-MAT2011 — Bachelor's Thesis (Overleaf source)

**Machine Learning & High Frequency Financial Time Series**
*Predicting short-term regime shifts via Hidden Markov Models*

**Author:** Egil Furnes — University of Oslo, Department of Mathematics
**Supervisor:** Associate Professor Gudmund Horn Hermansen

---

## Overview

This repository contains the LaTeX source for a bachelor's thesis investigating regime-switching models for high-frequency foreign exchange data. The core idea is to decompose EUR/USD tick prices into a latent efficient price and microstructure noise, then fit a Hidden Markov Model (HMM) with regime-switching AR dynamics to capture the switching between noise-dominated periods (bid-ask bounce) and momentum-driven price runs (order flow imbalance).

The companion code repository (data processing, model implementation, plots) is at [github.com/egil10/stk-mat2011](https://github.com/egil10/stk-mat2011).

---

## Repository structure

```
stk-mat2011-overleaf/
├── 00 MAIN.tex           # Master document — compile this
├── 01 FRONTMATTER.tex    # UiO front page configuration
├── 10 ABSTRACT.tex       # Abstract and acknowledgements
├── 10 INTRODUCTION.tex   # Introduction: microstructure effects, paper outline
├── 11 METHOD.tex         # Methods: price model, HMM, inference algorithms, metrics
├── 12 RESULT.tex         # Results: EDA of EUR/USD tick data (Jan 2026)
├── 13 CONCLUSION.tex     # Project plan / timeline
├── 19 APPENDIX.tex       # Appendix (placeholder)
├── 99 BIB.bib            # Bibliography (biblatex / biber)
├── 99 GRAVEYARD.tex      # Archived / commented-out content
├── plots/
│   └── eurusd_tick_analysis.pdf
├── article/              # Related reference PDF
└── uio/                  # University of Oslo document class and style files
    ├── uiobachelorthesis.cls
    ├── uiomasterfp.sty
    └── uiotools.sty
```

---

## Compiling

The document uses `biblatex` with `biber`. Compile with:

```
pdflatex "00 MAIN"
biber "00 MAIN"
pdflatex "00 MAIN"
pdflatex "00 MAIN"
```

Or open directly in [Overleaf](https://overleaf.com) — the project is synced there.

---

## Modelling framework (summary)

1. **Price decomposition** — observed tick price = latent efficient price + microstructure noise
2. **Pre-averaging** — smooth over blocks of $k$ ticks to attenuate noise before constructing returns
3. **Baseline AR(1)** — single-regime autoregressive benchmark
4. **HMM-SVAR** — $K$-state Hidden Markov Model where each regime has its own AR(1) dynamics; volatility extensions via regime-dependent ARCH/GARCH
5. **Inference** — Forward algorithm (likelihood), Viterbi algorithm (state decoding), Baum-Welch EM (parameter estimation)
6. **Model selection** — BIC over candidate values of $K$

---

## Data

EUR/USD tick data sourced from [HistData.com](https://www.histdata.com/). January 2026 sample (~48.5 M ticks across 32 currency pairs available in the companion repo).

---

## Status

| Month    | Task                                                                 |
|----------|----------------------------------------------------------------------|
| February | Literature review, data acquisition, pre-averaging implementation    |
| March    | Baseline AR model, HMM with regime-switching AR dynamics             |
| April    | Regime-dependent ARCH/GARCH, calibration and out-of-sample testing   |
| May 1–15 | Final results, write-up, code repository preparation                 |

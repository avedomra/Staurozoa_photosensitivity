# Life without eyes: behavioral evidence of photoreception in a stalked jellyfish *Haliclystus auricula* (Staurozoa)

This repository contains the data, analysis script, and output figures/tables for a study of light-evoked behaviour in stalked jellyfish (Staurozao, *Haliclystus auricula*). It accompanies the corresponding manuscript.

The analysis covers two parts:

1. **Control experiment** - spontaneous motor activity under two ambient light intensities (bright and dim), with no directed stimulus.
2. **Stimulus experiment** - probability of a motor response to focal illumination with red, green, and violet light applied to two body regions (calyx and stalk).

## Repository structure

```
.
├── data/
│   ├── control.xlsx           # Control experiment dataset
│   └── experiment.xlsx        # Stimulus experiment dataset
├── figures/                   # Generated figures (.png and .svg)
├── results/                   # Generated summary tables (.xlsx)
├── staurozoa_experiments.Rmd  # Full analysis script (R Markdown)
├── LICENSE
└── README.md
```

## Data description

### `data/control.xlsx`

Contains 334 movement events recorded across 8 specimens observed under two ambient light conditions (bright: specimens 1–4; dim: specimens 5–8). Each row represents a single movement event.

| Column     | Type      | Description |
|------------|-----------|-------------|
| `exp`      | character | Experiment ID |
| `light`    | factor    | Ambient light condition: `br` (bright) or `dim` (dim) |
| `spec`     | factor    | Specimen ID (1–8) |
| `start`    | numeric   | Event start time (s) |
| `stop`     | numeric   | Event stop time (s) |
| `type`     | factor    | Movement type: `rot`, `stalk`, `calyx`, or `full` |

(`duration` is computed in the script as `stop - start`.)

### `data/experiment.xlsx`

Contains 60 trials distributed across 9 experimental sessions, examining motor responses to focal red, green, and violet light stimulation of the calyx or stalk.

| Column         | Type      | Description |
|-----------------|-----------|-------------|
| `exp_no`        | factor    | Experimental session ID (9 levels) |
| `exp_ID`        | character | Unique trial identifier |
| `region`        | factor    | Body region stimulated: `calyx` or `stalk` |
| `light`         | factor    | Light colour: `R` (red), `G` (green), `V` (violet) |
| `time`          | factor    | Stimulus duration: `10` s or `30` s |
| `react`         | integer   | Binary: 1 = any motor response, 0 = no response |
| `react_no_rot`  | integer   | Binary: 1 = response excluding isolated calyx rotation |
| `react_type`    | character | Type of motor response (if `react = 1`) |

## Analysis script

`staurozoa_experiments.Rmd` is a self-contained R Markdown document that:

- Loads and tidies both datasets
- Produces timeline and summary figures for the control experiment
- Fits linear mixed-effects models (LMM) to assess effects of light intensity on movement duration
- Performs Wilcoxon rank-sum tests on movement frequency
- Fits (generalised) logistic models / GLMMs to assess effects of light colour and body region on response probability
- Applies Fisher's exact tests to examine the relationship between body region and response type
- Exports all figures to `figures/` and summary tables to `results/`

### Requirements

The script requires R (≥ 4.0) and the following packages:

```r
install.packages(c(
  "readxl", "ggplot2", "dplyr", "tidyr", "patchwork",
  "lme4", "lmerTest", "emmeans", "car", "DHARMa",
  "performance", "brglm2", "writexl", "ggsignif", "svglite"
))
```

## Citation

If you use this code or data, please cite the associated manuscript (citation details to be added upon publication).

## Contacts

- email: m.domracheva2000@yandex.ru
- GitHub: [@avedomra](https://github.com/avedomra)
- ResearchGate: [Maria Domracheva](https://www.researchgate.net/profile/Maria-Domracheva)

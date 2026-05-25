<p align="center">
  <img src="https://img.shields.io/badge/PsychoPy-v2024-green?style=for-the-badge&logo=python&logoColor=white&color=2C3930" />
  <img src="https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python&logoColor=white&color=3776AB" />
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" />
</p>

<h1 align="center">Fragile Visual Short-Term Memory<br>Feature Encodings of Shapes and Colors</h1>

<p align="center">
  <i>Does fragile VSTM preserve the detail of higher-order features more accurately than working memory?</i>
</p>

---

## Overview

Every time we look at a new scene, we feel as if we sense every detail at once. Yet this feeling of "seeing everything" is considered an illusion: we have limited capacity to report what we saw once we close our eyes (Naccache, 2018).

**Working Memory (WM)** retains only a small, non-detailed subset of visual information. But recent work has identified **fragile visual short-term memory (fVSTM)**, a store with near-perfect capacity that holds more detailed representations (Sligte et al., 2010), though it is short-lived and easily overwritten (Sligte et al., 2008).

Most prior studies compare objects that differ drastically (e.g. a pink pig vs. a red motorbike), making detection trivially easy. It remains unclear how well fVSTM encodes the fine-grained features of objects, and whether those encodings are truly detailed or merely gist-like (Block, 2011).

This experiment tests whether fVSTM encodes **shape** (square vs. circle) and **color** (green vs. blue) more accurately and faster than WM.

---

## Hypotheses

1. Since fVSTM is object-based, elementary features like shape and color should already be bound and well-encoded (Logie et al., 2008).

2. Prior work shows fVSTM encodes low-level features like orientation (Pinto et al., 2017). This study targets features formed later along the visual hierarchy (V2, V4, IT): **shapes and colors** (Perry & Fallah, 2014).


---

## Experimental Design

**Within-subjects**, adapted from Pinto et al. (2013) and Sligte et al. (2008).

| Factor | Levels |
|:--|:--|
| Memory type | fVSTM, WM |
| Feature change | Shape, Color |
| **DVs** | Accuracy (%), Reaction time (ms) |

### Stimuli

Eight items (squares and circles, green and blue) arranged on an imaginary circle (r = 300 px). Each feature type appears at least 3 times. No three adjacent items share the same shape or color.

<img width="1616" height="400" alt="image" src="https://github.com/user-attachments/assets/dd28fe18-2ffe-4299-89b5-2277c902a57d" />


| Property | Value |
|:--|:--|
| Square | 50 x 50 px, line width 5 |
| Circle | radius = sqrt(2500 / pi) px (equal area) |
| Green | RGB (0, 1, 0) |
| Blue | RGB (0, 0, 1) |
| Background | Black |
| Fixation | White circle, r = 6 px |
| Cue | White line pointing from center toward target |

### Trial Sequence

```
fVSTM Condition
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  Display (250 ms)  ➜  Blank (1000 ms)  ➜  Cue (500 ms)
  ➜  Blank (500 ms)  ➜  2nd Display  ➜  Response
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


WM Condition
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  Display (250 ms)  ➜  Blank (1000 ms)  ➜  2nd Display + Cue (500 ms)
  ➜  Response  ➜  If correct: "Shape or Color?"  ➜  Response
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Responses:** `Z` = change / shape, `M` = no change / color.

### Structure

- 1 practice block (8 trials, one per condition)
- 4 test blocks (80 trials each, 320 total)

Each block contains all 8 conditions (2 memory types x 2 change features + 4 stay trials), shuffled and repeated.

---

## Repository Structure

```
Feature-encoding-Visual-Short-term-Memory/
├── design_code.py          # Full PsychoPy experiment script
├── 01_tn_cape              # Example data: participant 01_tn
├── 01_on_cape              # Example data: participant 01_on
├── example data            # Placeholder
└── README.md
```

## Data Format

Each row is one trial. Columns (space-separated):

```
experiment  timestamp  participant_id  seed  age  gender  block  trial
change_state  change_feature  memory_type  accuracy_change  accuracy_feature  RT_ms
```

Example:
```
cape  2025-10-14_21h50.10.881  01_tn  326  20  female  0  2  change  color  fVSTM  1  0  1634.000
```

| Field | Description |
|:--|:--|
| `change_state` | `change` or `stay` |
| `change_feature` | `shape`, `color`, or `None` (if stay) |
| `memory_type` | `fVSTM` or `WM` |
| `accuracy_change` | 1 = correctly detected change/stay, 0 = incorrect |
| `accuracy_feature` | 1 = correctly identified shape vs color, 0 = incorrect |
| `RT_ms` | Reaction time in milliseconds |

---

## Running the Experiment

**Requirements:** Python 3.x with PsychoPy installed.

```bash
python design_code.py
```

A dialog box will prompt for participant ID, gender, age, and session number. Data is saved to `data/` in the working directory.

---

## References


- Block, N. (2011). Perceptual consciousness overflows cognitive access. *Trends in Cognitive Sciences, 15*(12), 567-575.
- Logie, R. H., Brockmole, J. R., & Vandenbroucke, A. R. E. (2008). Bound feature combinations in visual short-term memory are fragile but influence long-term learning. *Visual Cognition, 17*(1-2), 160-179.
- Naccache, L. (2018). Why and how access consciousness can account for phenomenal consciousness. *Phil. Trans. R. Soc. B, 373*(1755), 20170357.
- Perry, C. J., & Fallah, M. (2014). Feature integration and object representations along the dorsal stream visual hierarchy. *Frontiers in Computational Neuroscience, 8*.
- Pinto, Y., Sligte, I. G., Shapiro, K. L., & Lamme, V. A. F. (2013). Fragile visual short-term memory is an object-based and location-specific store. *Psychonomic Bulletin & Review, 20*(4), 732-739.
- Pinto, Y., Vandenbroucke, A. R., Otten, M., Sligte, I. G., Seth, A. K., & Lamme, V. A. F. (2017). Conscious visual memory with minimal attention. *Journal of Experimental Psychology: General, 146*(2), 214-226.
- Sligte, I. G. (2010). Detailed sensory memory, sloppy working memory. *Frontiers in Psychology, 1*.
- Sligte, I. G., Scholte, H. S., & Lamme, V. A. F. (2008). Are there multiple Visual Short-Term Memory Stores? *PLoS ONE, 3*(2), e1699.


---

<p align="center">
  <sub>Minh · University of Amsterdam · Psychology (Brain & Cognition)</sub>
</p>

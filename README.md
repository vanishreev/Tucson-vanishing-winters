# Tucson's Vanishing Winters — Watch the Blues Fade and Reds Take Over

**University of Arizona Data Visualization Challenge 2026**

Submitted by Vanishree Venkatachalapathy · March 18, 2026

---

## About

Tucson, Arizona sits in the Sonoran Desert — a city where summer heat is
expected, but where mild winters have long defined its character. This
project asks a simple question: *has that changed?*

Using 41 years of monthly NASA satellite temperature data (1984–2024),
this visualization tracks how Tucson's thermal fingerprint has shifted
across every month and every year of the record. Rather than a single
annual average, each month is measured against its own 41-year baseline —
so a warm January is judged on January's terms, not July's.

The answer is clear: the blues are fading. The reds are here to stay.

---

## Visualizations

Five complementary views of the same 41-year record:

| Visualization | What It Shows |
|---|---|
| **Warming Stripes** | One stripe per year, colored by annual mean anomaly — no axes, just the pattern |
| **Annual Anomaly Trend** | Year-by-year anomaly bars with a LOESS smoother revealing the long-term trajectory |
| **Monthly Heat Calendar** | All 492 month–year cells as a color grid — spot which months and seasons are shifting |
| **Monthly Warming Rose** | Polar chart showing which calendar months have warmed most relative to their own baselines |
| **Generative Particle Field** | An animated, interactive canvas encoding all 492 cells simultaneously as drifting particles |

### The Interactive Particle Field

The centerpiece visualization maps every (month, year) pair onto an
animated grid of particles:

- **Y-axis** — month of year (January at top → December at bottom)
- **X-axis** — year (1984 → 2024, left to right)
- **Color** — red = warmer than baseline · blue = cooler · amber = warm summer month (Jun–Aug)
- **Slider** — scrub through years to highlight a column
- **Hover** — hover over a month row to read the exact anomaly value
- **▶ Play** — animate through all 41 years automatically

---

## How to View

**No R installation required.** The rendered output is a single
self-contained HTML file.

1. Download `tucson-vanishing-winters.html` from the root of this repository
2. Open it in any modern web browser (Chrome, Firefox, Safari, Edge)

---

## How to Reproduce

To render the document from source:

**Requirements**
- R (≥ 4.1)
- Quarto (≥ 1.3)
- Internet connection (for the NASA POWER API call on first render)

**Install R packages**
```r
install.packages(c("nasapower", "dplyr", "tidyr", "lubridate", "jsonlite",
                   "htmltools", "ggplot2", "ggtext", "glue", "knitr", "scales"))
```

**Render**
```bash
quarto render tucson-vanishing-winters.qmd
```

> The data acquisition chunk calls the NASA POWER API live and caches
> the result. Subsequent renders use the cache and do not require an
> API call.

---

## Data

| Field | Detail |
|---|---|
| **Source** | NASA POWER Agroclimatology API |
| **Variable** | T2M — Monthly mean 2-metre air temperature (°C) |
| **Location** | Tucson, Arizona · 32.22°N, 110.97°W |
| **Period** | January 1984 – December 2024 |
| **Observations** | 492 (41 years × 12 months) |

---

## Methodology

**Temperature Anomalies**

Temperature anomalies are calculated on a **per-month basis**: each
observation is compared to that specific month's 41-year mean, not a
single annual average. This preserves the seasonal structure of the
warming signal — a warm January is judged against January's own average,
ensuring no month is penalized or rewarded by comparison to a different
season.

**Generative Particle Field Visualization**

The grid is divided into 41 columns (one per year) and 12 rows (one per
month), creating 492 cells. Each cell is assigned hundreds of small
moving dots — particles — that drift around their home cell in slow,
flowing motion. The color of each particle reflects the temperature
anomaly of its cell: red for warmer than average, blue for cooler, and
amber for warm summer months.

The flowing movement is generated using a hand-coded fractional Brownian
motion (fBm) noise algorithm — no external library. Think of it like
gentle wind gusts that nudge each particle in a slightly different
direction every frame, while an invisible elastic force keeps pulling it
back toward its home cell. The result is a visualization that feels alive
while remaining anchored to the underlying data.

---

## Tech Stack

| Layer | Tools |
|---|---|
| **Data retrieval** | R · `nasapower` |
| **Data wrangling** | R · `dplyr`, `tidyr`, `lubridate` |
| **Static visualization** | R · `ggplot2`, `ggtext`, `scales`, `glue` |
| **Interactive visualization** | Vanilla JavaScript · Canvas 2D API |
| **Noise algorithm** | Hand-coded fractional Brownian motion (fBm) · no external library |
| **R → JS bridge** | `jsonlite` (JSON export) · `htmltools` (iframe embed) |
| **Document** | Quarto HTML · self-contained single file |

---

## Repository Structure

```
tucson-vanishing-winters/
├── README.md
├── LICENSE
├── tucson-vanishing-winters.qmd            # Source document
├── tucson-vanishing-winters.html           # Self-contained rendered output
└── output/
    └── tucson-vanishing-winters-interactive.html   # Standalone interactive particle field
```

---

## Citation

**Data:**
NASA POWER Project. (2024). *Prediction of Worldwide Energy Resources
(POWER) — Agroclimatology Climatology Dataset*.
NASA Langley Research Center.
Retrieved from https://power.larc.nasa.gov/

**This project:**
Venkatachalapathy, V. (2026). *Tucson's Vanishing Winters: Watch the
Blues Fade and Reds Take Over*. University of Arizona Data
Visualization Challenge 2026.

---

## Author

**Vanishree Venkatachalapathy**
University of Arizona · Data Visualization Challenge 2026

---

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE)
for details.

---

## Acknowledgments

Temperature data provided by the NASA POWER Project, funded by the NASA
Earth Science Directorate Applied Science Program.

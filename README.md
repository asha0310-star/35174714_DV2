# Forests for Palm Oil — Malaysia's Trade-Off

FIT2179 Data Visualisation 2, Semester 1 2026. This single-page Vega-Lite story explains how Malaysia's palm oil economy connects to land expansion, tree-cover loss, and export demand. Live site: <https://asha0310-star.github.io/35174714_DV2/>.

## Domain, audience, and purpose

- **Domain:** Malaysia's palm oil industry and its environmental trade-off.
- **Audience:** A general Malaysian audience with no specialist statistics background.
- **Why:** Palm oil is economically important, but its landscape cost is uneven and difficult to understand from separate industry and forest datasets.
- **What:** The page combines palm oil production, planted-area, export, import-destination, and tree-cover-loss data.
- **How:** The story uses Munzer's What/Why/How framing through 15 presentation-focused Vega-Lite charts: annotated time series, a connected scatter plot, geographic maps, a state quadrant chart, a slopegraph, a heatmap, small multiples, a flow idiom, and a dual-direction trade-off chart.

## Assignment checklist

- Single scrollable web page: `index.html`.
- Vega-Lite JSON specifications are human-readable in `charts/`.
- Final page includes **15** charts/diagrams, including two geographic maps.
- Total cleaned data plus chart specs is small enough for GitHub Pages loading.
- Uses multiple independent sources: Our World in Data, MPOB, and Global Forest Watch.
- AI use and data caveats are acknowledged in the page footer.
- Public GitHub Pages URL: <https://asha0310-star.github.io/35174714_DV2/>.

## Final chart set and removals

The final webpage keeps 15 charts: global production lines, recent producer ranking, efficiency metric, indexed production/area trend, connected scatter, state quadrant, choropleth map, loss-intensity dot plot, layered map, dual trade-off chart, state ranking slopegraph, state-year heatmap, national forest-loss line, state small multiples, and export flow diagram.

Removed from the final page to reduce repetition and label/legend crowding:

- `chart04_malaysia_share_line.json` — repeated the global-market message already covered by the global production chart and recent producer ranking.
- `chart05_slope_landuse.json` — useful context, but less central than the Malaysia production/area and forest-pressure charts.
- `chart07_state_stacked_area.json` — regional production/area comparison is now better handled by the layered map and state quadrant.
- `chart15_importer_rank.json` — duplicated the top-importer message shown more distinctively by the Vega-Lite flow diagram.

## Data sources

| Source                                                                                                                                               | Files used/generated                                                                                                                                                                | Purpose                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| Our World in Data — Palm Oil (`raw/palm-oil-production(Our World in Data).csv`, `raw/land-use-palm-oil.csv`)                                         | `data/palm_production_long.csv`, `data/landuse_slope.csv`                                                                                                                           | Long-run global production and harvested-area context.                                                   |
| Malaysian Palm Oil Board overview reports (`raw/Annual Overview Reports Overview 2024.pdf` and public 2025 overview figures typed into `wrangle.py`) | `data/malaysia_yearly.csv`, `data/production_area_index.csv`, `data/malaysia_palmoil_kpi.csv`, `data/state_cpo_2025.csv`, `data/top_importers_2025.csv`, `data/imports_flows.csv`, `data/malaysia_economy_yearly.csv` | Malaysia production, planted area, regional 2025 production, export values, and top export destinations. |
| MPOB Oil Palm Planted Area 2025 state table (`https://bepi.mpob.gov.my/images/area/2025/Area_summary2025.pdf`) | `data/state_planted_area_2025.csv`, used with GFW-derived totals in `data/state_tradeoff_2025.csv` | State-level 2025 oil-palm planted area for the quadrant trade-off chart. |
| Global Forest Watch (`raw/Global Forest Watch Data.xlsx`)                                                                                            | `data/forest_loss_by_state_long.csv`, `data/forest_loss_state_totals.csv`, `data/state_loss_intensity.csv`, `data/area_vs_loss_yearly.csv`, `data/state_loss_rank_change.csv`                                                                           | State and national tree-cover loss, 2001–2024.                                                           |
| Malaysia TopoJSON (`data/malaysia_states.topojson`)                                                                                                  | used directly by `charts/map08_choropleth_states.json` and `charts/map09_layered_map.json`                                                                                          | Geographic state boundaries for Vega-Lite maps.                                                          |

## Data caveats

- Global Forest Watch tree-cover loss is not identical to permanent deforestation. It can include timber harvest and plantation rotations.
- The project uses tree-cover loss and palm oil production together to show overlap and timing, not exact hectare-by-hectare causality.
- OWID's long-run production series currently ends at 2023, while MPOB industry data in this repository includes 2025 values. Linked global context therefore caps selected-year markers at 2023 where the OWID series ends.
- MPOB PDF values that are not provided as machine-readable CSV are typed into `wrangle.py` with comments and mirrored in the small cleaned CSV files.
- `data/state_tradeoff_2025.csv` is derived by joining MPOB 2025 state planted-area values with existing GFW state tree-cover-loss totals. Federal territories without MPOB oil-palm planted-area rows are excluded from this palm-state comparison.
- `data/state_loss_rank_change.csv` is derived from `data/forest_loss_by_state_long.csv` by ranking each state in the earliest and latest available years (2001 and 2024).

## 2026 polish change log

- Upgraded the centrepiece connected scatter plot with key-year annotations for the peak tree-cover-loss year, largest planted-area year in the joined series, and the latest forest-loss year.
- Added a custom state trade-off quadrant chart comparing 2025 oil-palm planted area with 2001–2024 tree-cover loss.
- Added a state ranking slopegraph comparing tree-cover-loss rankings in 2001 and 2024.
- Reworked section headings, chart explanations, callouts, map-method note, and footer metadata to strengthen the single-scroll story and academic acknowledgement.
- Improved responsive layout and typography while keeping all charts in Vega-Lite v5 JSON files and all downloadable derived datasets small.
- Final QA pass reduced the public page from 19 to 15 charts by removing four repetitive/basic charts and keeping the strongest custom idioms.

## Hand-drawn sketch

**Before submission, add a hand-drawn sketch as `sketch.pdf`.** This file is currently not present in the repository. It should be a real hand-drawn planning sketch that has been scanned or photographed and then linked/submitted through Moodle/GitHub; do not replace it with a digitally generated sketch.

## Run locally

Because Vega-Lite loads local CSV/JSON files, use a local web server instead of opening `index.html` directly from the filesystem.

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000/>.

## Regenerate data

```bash
python3 -m pip install -r requirements.txt
python3 wrangle.py
```

The cleaned files are committed in `data/` so the public page works without running Python.

## Repository structure

```text
index.html          Main single-page visualisation
css/style.css       Page layout and visual styling
charts/*.json       Vega-Lite chart/map specifications
data/*.csv          Cleaned small datasets used by Vega-Lite
raw/*               Original downloaded/source files used for reproducibility
wrangle.py          Script that regenerates cleaned datasets
requirements.txt    Python dependencies for wrangling
```

## AI acknowledgement

Generative AI tools (Claude and ChatGPT) were used for proofreading, draft Vega-Lite structures, and debugging assistance. All data selection, wrangling, chart design choices, story structure, and final code remain the author's own work.

## Authorship

Created by Abdul Hakim Shaon, May 2026, for FIT2179 Data Visualisation 2 at Monash University Malaysia.

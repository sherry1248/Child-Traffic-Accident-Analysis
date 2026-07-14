# Child Traffic Accident and School Zone Analysis

A data analysis and visualization project that preprocesses child traffic accident and school zone data, compares accidents occurring inside and outside school zones, and visualizes accident locations and injury severity using interactive maps and charts.

The project mainly focuses on traffic accident data from Gyeonggi Province between 2017 and 2022. It also includes address geocoding, regional risk-score experiments, Folium map generation, and Korean news text analysis using word clouds.

> This repository is an exploratory data analysis project containing Jupyter Notebooks, Python scripts, intermediate datasets, and generated visualization results. It is not a complete web service or installable software package.

---

## Project Overview

The main objective of this project is to analyze child traffic accidents and evaluate their relationship with designated school zones.

The project performs the following tasks:

* Preprocesses child traffic accident data from 2017 to 2022
* Identifies whether each accident occurred inside or outside a school zone
* Analyzes accident patterns by year, month, day, time, and injury severity
* Converts addresses into geographic coordinates
* Visualizes accident locations and school zones on interactive maps
* Calculates experimental regional risk scores using weighted injury severity
* Collects child traffic accident news articles and generates Korean word clouds

---

## Key Features

### 1. Accident Data Preprocessing

The project compares complete child accident records with school-zone accident records.

It uses accident IDs to classify records into:

* Accidents inside school zones
* Accidents outside school zones

The notebooks also divide accident timestamps into year, month, date, and hour for time-based analysis.

Main files:

* `mid_project_3.ipynb`
* `code/mid_project_3 copy.ipynb`
* `num-data/0cbf7c1bf7bcb2f8.ipynb`
* `mid_project_3 map.ipynb`

---

### 2. Address Geocoding

Addresses are converted into longitude and latitude values using the VWorld Address Search API.

The converted coordinates are saved as Excel files and later used for map visualization.

Main files:

* `project2_2.py`
* `code/mid_project.ipynb`

---

### 3. Risk Analysis and Map Visualization

The project calculates regional risk scores by applying different weights to accident counts based on injury severity.

Accident locations are displayed using:

* Folium markers
* Circle markers
* Heatmaps
* GeoJSON school-zone layers
* OpenStreetMap road networks
* Grid-based accident-density analysis

Main files:

* `mid_ln.py`
* `mid_ln_test.py`
* `mid_project_map.ipynb`

Generated map examples are stored in:

* `all_maps.html`
* `data/file/*.html`

---

### 4. News Analysis and Word Cloud

The project collects Korean news articles related to child traffic accidents using the Naver News Search API.

Korean nouns are extracted using KoNLPy's `Okt`, filtered with stopword lists, and visualized using WordCloud.

Main files:

* `code/project_1.py`
* `code/project1.ipynb`

Example outputs:

* `data/어린이교통사고 - 네이버API 뉴스검색.csv`
* `data/save.png`

---

## Project Structure

```text
Midproject-master/
├── README.md
├── mid_ln.py
├── mid_ln_test.py
├── project2_2.py
├── mid_project_3.ipynb
├── mid_project_3 map.ipynb
├── mid_project_map.ipynb
├── code/
│   ├── mid_project.ipynb
│   ├── project1.ipynb
│   ├── project_1.py
│   ├── mid_project_3 copy.ipynb
│   └── mid_project_map_backup.ipynb
├── data/
│   ├── *.xlsx
│   ├── *.csv
│   ├── *.shp
│   ├── *.shx
│   ├── *.dbf
│   ├── output.geojson
│   ├── pos_pol_word.txt
│   ├── neg_pol_word.txt
│   ├── save.png
│   └── file/
├── num-data/
│   ├── *.xls
│   ├── *.xlsx
│   ├── *.csv
│   └── 0cbf7c1bf7bcb2f8.ipynb
├── gyeonggi_protect_polygons*.geojson
├── 서울어린이보호구역 위치도.json
├── all_maps.html
└── *.xlsx, *.csv
```

The repository contains original data, processed copies, experimental files, and generated outputs. File paths and input datasets should be checked before running each notebook or script.

---

## Technology Stack

| Area                    | Technologies                      |
| ----------------------- | --------------------------------- |
| Data Processing         | Python, pandas, NumPy             |
| Data Visualization      | Matplotlib, Seaborn, Plotly       |
| Interactive Maps        | Folium, Branca                    |
| Spatial Analysis        | GeoPandas, Shapely, OSMnx, GeoPy  |
| Text Analysis           | KoNLPy, WordCloud                 |
| API Integration         | VWorld API, Naver News Search API |
| Development Environment | Jupyter Notebook                  |

---

## Requirements

Python 3 and a Jupyter environment are required.

Main dependencies:

```text
pandas
numpy
openpyxl
xlrd
matplotlib
seaborn
plotly
folium
branca
geopandas
shapely
osmnx
geopy
requests
konlpy
wordcloud
Pillow
jupyter
```

KoNLPy may require an additional Java installation depending on the operating system.

---

## Installation

Clone the repository and move into the project directory.

```bash
git clone <repository-url>
cd Midproject-master
```

Create a virtual environment.

```bash
python -m venv .venv
```

Activate it on macOS or Linux:

```bash
source .venv/bin/activate
```

Activate it on Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Install the required packages.

```bash
python -m pip install --upgrade pip
python -m pip install pandas numpy openpyxl xlrd matplotlib seaborn plotly folium branca geopandas shapely osmnx geopy requests konlpy wordcloud Pillow jupyter
```

---

## Before Running

Some scripts and notebooks contain absolute Windows paths from the original development environment, such as:

```text
C:\sqlite\mysql\code\AI\...
```

These paths must be replaced with paths that match the local project structure.

Example:

```python
# Original
pd.read_excel(
    'C:\\sqlite\\mysql\\code\\AI\\Mid_project\\data\\file\\all_test - 복사본.xlsx'
)

# Recommended relative path
pd.read_excel('data/file/all_test - 복사본.xlsx')
```

Output paths should also be changed in the same way.

VWorld and Naver API credentials must be replaced with valid user credentials. API keys should not be committed to Git and should be managed through environment variables or a separate configuration file.

---

## Usage

### Run the Jupyter Notebooks

Start Jupyter Notebook from the project root.

```bash
jupyter notebook
```

A recommended analysis order is:

1. `num-data/0cbf7c1bf7bcb2f8.ipynb`
2. `code/mid_project_3 copy.ipynb`
3. `mid_project_3.ipynb`
4. `mid_project_3 map.ipynb`
5. `mid_project_map.ipynb`

The notebooks are not connected through an automated pipeline. Required input files should be checked before running each notebook.

---

### Generate the Risk Map

After adjusting the file paths, run:

```bash
python mid_ln.py
```

The experimental OSMnx and grid-based map script can be run with:

```bash
python mid_ln_test.py \
  --accidents_csv "data/file/merged_dataframe.csv" \
  --A_IDs "수원시 장안구" \
  --distance 250 \
  --grid_size 6
```

If `--A_IDs` is omitted, the script processes all unique regions from the `시군구` column.

This script downloads OpenStreetMap road-network data and therefore requires an internet connection.

---

### Run Address Geocoding

Configure the input path, output path, and VWorld API credentials in `project2_2.py`.

```bash
python project2_2.py
```

The script reads addresses from the `시군구` column, removes text inside parentheses, retrieves longitude and latitude values, and saves the result as an Excel file.

---

### Run News and Word Cloud Analysis

Configure the Naver API credentials, dataset paths, and Korean font path in `code/project_1.py`.

```bash
python code/project_1.py
```

The script saves retrieved news results as a CSV file and generates a Korean word-cloud image.

---

## View Generated Maps

The generated HTML maps can be opened directly in a browser.

A simple local server can also be used:

```bash
python -m http.server 8000
```

Open the following address:

```text
http://localhost:8000/all_maps.html
```

Other generated maps under `data/file/` can be viewed in the same way.

---

## Visualization Outputs

The map visualizations include:

* Child traffic accident locations
* Accident counts by region
* Injury-severity distributions
* Weighted regional risk scores
* School-zone boundaries
* Accident-density heatmaps
* OpenStreetMap road networks

---

## Limitations

* Several scripts contain environment-specific Windows paths.
* The repository does not include a `requirements.txt` file.
* There is no automated test suite or integrated execution pipeline.
* `mid_ln.py` and `mid_ln_test.py` use different risk-score formulas and should not be interpreted as identical indicators.
* OSMnx map generation may fail depending on the availability of road-network data.
* API-dependent functions require valid credentials and internet access.
* The WordCloud script assumes a Windows Korean font path such as `malgun.ttf`.
* The redistribution rights of included public, map, and news datasets should be checked separately.

---

## Security Notice

Any API credentials that were previously included in the source code should be considered exposed.

Before using the project:

* Revoke old API credentials
* Generate new credentials
* Store them in environment variables
* Add secret files to `.gitignore`

Example:

```text
.env
config.py
secrets.json
```

---

## Project Outcomes

This project demonstrates the complete workflow of a geospatial data analysis project:

* Multi-year traffic accident data preprocessing
* School-zone accident classification
* Temporal and injury-severity analysis
* Address geocoding
* Geographic data integration
* Interactive map visualization
* Experimental risk-score design
* Korean news text analysis

It also highlights practical challenges such as inconsistent data formats, API integration, environment-specific paths, geospatial processing, and visualization of large datasets.

---

## Future Improvements

* Replace absolute paths with configurable relative paths
* Add a `requirements.txt` file
* Create a unified preprocessing and analysis pipeline
* Standardize the regional risk-score formula
* Move API credentials to environment variables
* Add automated data validation
* Build an interactive dashboard using Streamlit or Dash
* Improve school-zone risk comparison using statistical analysis

---

## License

This repository does not currently include a license file.

Unless a license is added, permission to use, modify, or redistribute the source code is not explicitly granted.

The terms of use for public datasets, map data, and news data included in the project should also be reviewed separately.

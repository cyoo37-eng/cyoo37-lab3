# COVID-19 Data Visualization in the United States (2020)

## Project Description
This project presents two interactive web maps visualizing COVID-19 data across the United States for the year 2020. The visualizations help users understand both the spread and intensity of COVID-19 cases at the county level.

## Project Links
- **Map 1 - Choropleth Map (Rates):** [View Map](https://[your_github_username].github.io/[your_repository_name]/map1.html)
- **Map 2 - Proportional Symbols Map (Cases):** [View Map](https://[your_github_username].github.io/[your_repository_name]/map2.html)

## Screenshots

### Map 1: COVID-19 Rates (Choropleth Map)
![Choropleth Map Screenshot](img/map1-screenshot.png)

*This choropleth map displays COVID-19 case rates per 1,000 residents across U.S. counties. Darker colors indicate higher infection rates.*

### Map 2: COVID-19 Cases (Proportional Symbols Map)
![Proportional Symbols Map Screenshot](img/map2-screenshot.png)

*This proportional symbols map shows total COVID-19 cases, with larger circles representing counties with more cases.*

## Maps Overview

### Map 1: Choropleth Map - COVID-19 Rates
- **Purpose:** Visualize the intensity of COVID-19 spread normalized by population
- **Data:** Case rates per 1,000 residents
- **Projection:** Albers USA
- **Basemap:** Mapbox Light (for better contrast with colored polygons)
- **Color Scheme:** Sequential color palette from yellow to red
- **Interactive Features:**
  - Click on any county to view detailed rate information
  - Hover effects with cursor changes
  - Pop-up displays county name, state, and case rate

### Map 2: Proportional Symbols Map - COVID-19 Cases
- **Purpose:** Show the absolute magnitude of COVID-19 cases
- **Data:** Total COVID-19 cases per county
- **Projection:** Albers USA
- **Basemap:** Mapbox Dark (for better symbol visibility)
- **Symbol Design:** Graduated circles with color gradients
- **Interactive Features:**
  - Click on circles to view total case counts
  - Hover effects with cursor changes
  - Pop-up displays county name, state, and total cases

## Primary Functions

### 1. **Albers Projection Implementation**
Both maps use the Albers equal-area conic projection, which is ideal for mapping the continental United States as it minimizes distortion:

```javascript
projection: 'albers'
```

### 2. **Choropleth Mapping with Step Expressions**
Map 1 uses Mapbox's expression syntax to create data-driven styling for the choropleth visualization:

```javascript
'fill-color': [
    'step',
    ['get', 'rates'],
    colors[0],
    grades[1], colors[1],
    grades[2], colors[2],
    // ... additional steps
]
```

### 3. **Proportional Symbol Sizing**
Map 2 implements proportional symbols where circle radius corresponds to case counts using property-based stops:

```javascript
'circle-radius': {
    'property': 'cases',
    'stops': [
        [grades[0], radii[0]],
        [grades[1], radii[1]],
        // ... additional stops
    ]
}
```

### 4. **Interactive Popups**
Both maps feature click-event listeners that display detailed information:

```javascript
map.on('click', 'layer-id', (e) => {
    new mapboxgl.Popup()
        .setLngLat(e.lngLat)
        .setHTML(content)
        .addTo(map);
});
```

### 5. **Dynamic Legend Generation**
Custom legends are programmatically generated using JavaScript to match the map symbology.

## Libraries and Tools

- **Mapbox GL JS v2.8.1:** Web mapping library for rendering interactive maps
- **HTML5 & CSS3:** Structure and styling
- **JavaScript (ES6):** Interactive functionality and data visualization
- **Google Fonts (Open Sans):** Typography
- **GeoJSON:** Spatial data format

## Data Sources

1. **COVID-19 Case Data:** 
   - Source: [The New York Times COVID-19 Data Repository](https://github.com/nytimes/covid-19-data)
   - Coverage: All U.S. counties, 2020
   - Processed to include rates and total counts

2. **Population Data:**
   - Source: U.S. Census Bureau, 2018 ACS 5-Year Estimates
   - Used to calculate case rates per 1,000 residents

3. **County Boundaries:**
   - Source: U.S. Census Bureau
   - Format: Converted to GeoJSON and simplified using Mapshaper

## Data Processing

The original shapefiles were processed using the following steps:
1. Converted from shapefile to GeoJSON format
2. Reprojected to WGS84 (EPSG:4326) for web mapping
3. Simplified geometries using Mapshaper to reduce file size
4. Removed unnecessary attributes to optimize performance
5. Calculated case rates: (total cases / population) × 1000

## File Structure

```
covid-19-map-visualization/
├── map1.html                    # Choropleth map
├── map2.html                    # Proportional symbols map
├── README.md                    # Project documentation
├── assets/
│   ├── us-covid-2020-rates.geojson    # COVID rates data
│   └── us-covid-2020-counts.geojson   # COVID cases data
├── css/
│   └── style.css               # Stylesheet
├── img/
│   ├── map1-screenshot.png     # Map 1 screenshot
│   └── map2-screenshot.png     # Map 2 screenshot
└── js/
    └── (optional external scripts)
```

## Setup Instructions

1. **Get a Mapbox Access Token:**
   - Sign up for a free account at [Mapbox](https://www.mapbox.com/)
   - Navigate to your account page and copy your access token
   - Replace `'YOUR_MAPBOX_TOKEN_HERE'` in both `map1.html` and `map2.html` with your token

2. **Prepare the Data:**
   - Unzip `us-covid-2020.zip`
   - Convert shapefiles to GeoJSON (if not already done)
   - Place GeoJSON files in the `assets/` folder

3. **Test Locally:**
   - Use a local server (e.g., VS Code Live Server, Python's http.server)
   - Open `map1.html` and `map2.html` in your browser

4. **Deploy to GitHub Pages:**
   - Create a new GitHub repository
   - Push all files to the repository
   - Enable GitHub Pages in repository settings (select main branch)
   - Access maps via: `https://[username].github.io/[repo-name]/map1.html`

## Acknowledgments

- Lab design and data processing: Steven Bao, Bo Zhao (University of Washington)
- COVID-19 data: The New York Times
- Census data: U.S. Census Bureau
- Mapping technology: Mapbox
- Course: GEOG 458 - Advanced Digital Geographies

## Credits

Created as part of Lab 3 for GEOG 458 at the University of Washington.

**Author:** [Your Name]  
**Date:** January 2026  
**Instructor:** Bo Zhao

---

*For questions or issues, please open an issue in this repository.*

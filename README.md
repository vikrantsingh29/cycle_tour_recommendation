
# Cycling Tour Recommendation System 🚴

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Example Queries](#example-queries)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Flow Diagram](#flow-diagram)
- [Author](#author)

## Introduction
Welcome to the **Cycling Tour Recommendation System**! This project is designed to help cycling enthusiasts find the most suitable cycling routes based on their preferences and requirements. Whether you're a beginner looking for easy trails, a family seeking safe routes, or an experienced rider craving challenging paths, this system has got you covered.

Leveraging Natural Language Processing (NLP), geospatial analysis, and data filtering techniques, the application interprets your natural language queries to provide personalized cycling route recommendations in the Tyrol region.

## Features 🚀
- **Natural Language Query Handling:** Input your preferences in plain English, and the system interprets your needs.
- **Customized Recommendations:** Filters routes based on location, difficulty level, route length, elevation gain, user type, and seasonal availability.
- **Interactive Map Visualization:** View recommended routes on an interactive map with start and end points clearly marked.
- **User Type Constraints:** Tailored recommendations for different user types such as families, beginners, and enthusiasts.
- **Proximity Search:** Find routes near a specified location within a defined radius.

## Installation 🔧

### Prerequisites
- [Python 3.7+](https://www.python.org/downloads/)
- [Jupyter Notebook](https://jupyter.org/install)

### Clone the Repository
```bash
git clone https://github.com/yourusername/cycling-tour-recommendation.git
cd cycling-tour-recommendation
```

### Install Dependencies
It's recommended to use a virtual environment.

```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Upgrade pip
pip install --upgrade pip

```

```bash
pip install pandas geopy folium spacy transformers torch nltk scikit-learn
```

### Download SpaCy Model
```bash
python -m spacy download en_core_web_sm
```

## Usage 🚴‍♂️
1. **Launch Jupyter Notebook:**

   ```bash
   jupyter notebook
   ```

2. **Open the Notebook:** Navigate to the `Cycling_Tour_Recommendation.ipynb` file and open it.

3. **Load the Data:** Ensure the GeoJSON data file (`cycling_tours.geojson`) is in the same directory as the notebook. Run the data loading cell.

4. **Enter Your Query:** Locate the cell designated for inputting queries. Enter your natural language query related to cycling routes.

5. **Run the Query:** Execute the cell to process your query. The system will display matching cycling tours based on your input.

6. **View on Map:** After running the query, an interactive map will be generated, visualizing the recommended routes.

## Example Queries 🔍
Here are some sample queries you can try:

- **Basic Query:**
  ```
  List me all the cycling routes.
  ```

- **Seasonal Availability:**
  ```
  List me the cycling routes for summer.
  ```

- **Location-Based Query:**
  ```
  Find cycling tours near Kufstein with a route length more than 10km and elevation gain less than 500 meters.
  ```

- **User Type Specific:**
  ```
  Find cycling routes near Landeck suitable for families.
  ```

- **Combined Criteria:**
  ```
  Find cycling routes near Schwaz with route length over 30km and elevation gain over 800 meters.
  ```

- **Difficulty and Season:**
  ```
  Find cycling routes that are loop tours available in September.
  ```


## Sample Map View 🗺️
![Sample Map View](https://github.com/vikrantsingh29/cycle_tour_recommendation/blob/main/map2.png)

## Technologies Used 🛠️
- **Python Libraries:**
  - `pandas` - Data manipulation and analysis.
  - `geopy` - Geocoding and distance calculations.
  - `folium` - Interactive map visualization.
  - `spaCy` - Natural Language Processing.
  - `transformers` - BERT-based models for NER and classification.
  - `nltk` - Natural Language Toolkit for text processing.

- **Machine Learning Models:**
  - **BERT-Based NER:** For extracting entities like locations from user queries.
  - **Zero-Shot Classification (BART):** For determining difficulty levels based on user descriptions.
 
- ** Sample query and output with query processing **
 ```
  --- Query 1:-Find cycling routes near Kufstein with route length over 5km suiable for families.

Parsed Criteria: {'type': None, 'location': 'Kufstein', 'user_type': 'family', 'difficulty_levels': None, 'preferred_month': None, 'min_route_length_km': 5.0, 'max_route_length_km': None, 'min_elevation_gain': None, 'max_elevation_gain': None}
Initial number of tours: 249
Number of tours after proximity filter: 159
Number of tours after applying minimum route length (5.0 km): 149
Number of tours after applying family-specific constraints: 18
Number of top tours selected: 5
Matching Cycling Tours:

Tour Name: MTB-Tour 349 Söll-Hintersteiner See
Route Length: 9.4 km
Difficulty Level: 1
Elevation Gain: 430.0 meters
Tour Type: Single
Round Trip: No
Available Months: May, June, July, August, September, October
Coordinates: Start at (47.50358, 12.19169), End at (47.54254, 12.22356)

Tour Name: Söll - Stallhäusl
Route Length: 6.1 km
Difficulty Level: 1
Elevation Gain: 310.0 meters
Tour Type: Single
Round Trip: No
Available Months: April, May, June, July, August, September, October
Coordinates: Start at (47.50349, 12.19157), End at (47.48997, 12.14285)

Tour Name: MTB-Tour 350 Söll-Hochsöll
Route Length: 5.1 km
Difficulty Level: 1
Elevation Gain: 480.0 meters
Tour Type: Single
Round Trip: No
Available Months: May, June, July, August, September, October
Coordinates: Start at (47.50358, 12.19168), End at (47.48099, 12.1981)

Tour Name: Rundfahrt zur Wallfahrtskirche Mariastein
Route Length: 6.1 km
Difficulty Level: 1
Elevation Gain: 148.0 meters
Tour Type: Single
Round Trip: Yes
Available Months: May, June, July, August, September, October
Coordinates: Start at (47.52646, 12.0537), End at (47.49302, 12.05566)

Tour Name: MTB-Tour 265 Hochsöll-Brixen im Thale
Route Length: 9.3 km
Difficulty Level: 1
Elevation Gain: 200.0 meters
Tour Type: Single
Round Trip: No
Available Months: May, June, July, August, September, October
Coordinates: Start at (47.48099, 12.1981), End at (47.45026, 12.24609)
  ```

## Project Structure 📁

```plaintext
cycling-tour-recommendation/
│
├── Cycling_Tour_Recommendation.ipynb
├── cycling_tours.geojson
├── README.md
└── LICENSE
```

- `Cycling_Tour_Recommendation.ipynb`: Main Jupyter Notebook containing the implementation.
- `cycling_tours.geojson`: GeoJSON file with cycling tour data.
- `README.md`: Project documentation.
- `LICENSE`: License information.

## Flow Diagram 📊
### Query Processing Workflow
```mermaid
graph TD
    A[User Inputs Query] --> B[parse_query Function]
    B --> C[Apply Filters]
    C --> D[Rank and Select Top N Tours]
    D --> E[Present Results to User]
    E --> F[Display Interactive Map]
    
    style A fill:#fff,stroke:#000,stroke-width:2px
    style B fill:#fff,stroke:#000,stroke-width:2px
    style C fill:#fff,stroke:#000,stroke-width:2px
    style D fill:#fff,stroke:#000,stroke-width:2px
    style E fill:#fff,stroke:#000,stroke-width:2px
    style F fill:#fff,stroke:#000,stroke-width:2px
```

## Author 👤
- **Vikrant Singh**


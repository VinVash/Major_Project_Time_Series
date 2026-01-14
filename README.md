# Major Project

A full-stack application for time series data analysis and clustering with an interactive web interface.

## Project Overview

This project consists of a Flask backend for time series clustering and analysis, and a React frontend for visualization and interaction. The backend uses machine learning algorithms to cluster time series data, identify peaks and valleys, and perform outlier detection.

## CSV File Format Requirements

The application accepts CSV files with the following specifications:

### Format
- **Separator**: Comma-separated values (`,`)
- **Encoding**: UTF-8 (standard)
- **Header**: Optional (if present, will be ignored)

### Data Structure
- **Each row** represents a single time series (one graph/series)
- **Each column** represents a time point/measurement
- **All values** must be numeric (integers or floats)
- The data is processed row-wise, where each row is treated as an independent time series

### Data Requirements
- All cells must contain valid numeric values (no text, no empty cells)
- Missing values are not supported - ensure all cells are filled
- The number of columns (time points) should be consistent across all rows
- Rows with less than 4 peaks after processing will be automatically filtered out

### Example Format
```
266,270,273,269,271,270,268,269,269,270,...
264,265,265,264,263,264,263,264,264,262,...
328,324,325,323,324,323,323,319,324,324,...
```

In this example:
- Row 1, Row 2, Row 3 each represent a different time series
- Each comma-separated value represents a measurement at a specific time point
- All values are numeric

### Processing Notes
- The uploaded data undergoes preprocessing including:
  - Derivative calculation
  - Normalization (mean-centered and scaled)
  - Peak detection (rows with < 4 peaks are removed)
  - Outlier detection using Local Outlier Factor
- The processed data is then used for clustering analysis

## Project Structure

```
MajorProjectBackend/
├── backend/          # Flask backend server
│   ├── server.py     # Main backend application
│   └── requirements.txt
└── frontend/         # React frontend application
    ├── src/          # React source code
    └── package.json
```

## Backend

### Technology Stack
- **Flask** - Web framework
- **TimeSeriesKMeans** (tslearn) - Time series clustering
- **scikit-learn** - Machine learning utilities
- **NumPy & Pandas** - Data processing
- **SciPy** - Signal processing (peak detection)

### Features
- Time series data upload and processing
- Automatic optimal cluster determination using Elbow Method
- Outlier detection using Local Outlier Factor
- Peak and valley detection
- Dynamic clustering with further cluster refinement
- Graph labeling (true/false) for clusters
- Reference graph identification

### Setup

1. Navigate to the backend directory:
```bash
cd MajorProjectBackend/backend
```

2. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Run the server:
```bash
python server.py
```

The backend server will run on `http://0.0.0.0:5000` or on the URL indicated in the terminal.

### API Endpoints

- `POST /upload` - Upload CSV file for processing
- `POST /furtherCluster?cluster_no=<id>` - Further cluster a specific cluster
- `GET /getNoOfClusters` - Get the number of clusters
- `GET /getFarthestGraph?graph_id=<id>` - Get the farthest graph in a cluster
- `GET /getClosestGraph?graph_id=<id>` - Get the closest graph in a cluster
- `GET /labelTrue?graph_id=<id>` - Label a cluster as true
- `GET /labelFalse?graph_id=<id>` - Label a cluster as false
- `GET /getSeries` - Get the processed time series data
- `GET /getLabelGraphId` - Get labels and cluster IDs

## Frontend

### Technology Stack
- **React** - UI framework
- **Chart.js** - Data visualization
- **Axios** - HTTP client
- **Tailwind CSS** - Styling
- **PapaParse** - CSV parsing

### Features
- Interactive time series visualization
- Cluster visualization and exploration
- Peak and valley highlighting
- Graph comparison tools
- Cluster labeling interface

### Setup

1. Navigate to the frontend directory:
```bash
cd MajorProjectBackend/frontend
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm start
```

The frontend will run on `http://localhost:3000` and automatically open in your browser.


## Getting Started

1. **Start the backend server:**
   ```bash
   cd MajorProjectBackend/backend
   python server.py
   ```

2. **Start the frontend (in a new terminal):**
   ```bash
   cd MajorProjectBackend/frontend
   npm start
   ```

3. **Access the application:**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5000


## License

This project is part of a Major Project for academic purposes.


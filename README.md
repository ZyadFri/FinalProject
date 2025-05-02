# CPU Scheduler Simulator

**CPU Scheduler Simulator** is a web-based application for simulating, visualizing, and comparing multiple CPU scheduling algorithms. It combines a Python Flask backend with a React frontend to provide interactive Gantt‑chart visualizations and performance metrics for each algorithm.

---

## Table of Contents

1. [Project Structure](#project-structure)
2. [Features](#features)
3. [Technologies Used](#technologies-used)
4. [Installation](#installation)

   * [Backend Setup](#backend-setup)
   * [Frontend Setup](#frontend-setup)
5. [Usage](#usage)

   * [Generate Processes](#generate-processes)
   * [Run a Simulation](#run-a-simulation)
   * [View Results](#view-results)
   * [Compare Algorithms](#compare-algorithms)
6. [API Reference](#api-reference)
7. [Contributing](#contributing)
8. [License](#license)

---

## Project Structure

```bash
backend/                 # Flask API and scheduling logic
├── api.py               # REST endpoints for process generation and results
├── scheduler_adapter.py # Converts between API and algorithm implementations
├── scheduler_impl/      # Python modules implementing scheduling algorithms
└── jobs/                # Auto-created directory to store generated job files

frontend/                # React application for UI and visualizations
├── public/              # Static public assets (index.html, logo, etc.)
├── src/
│   ├── components/      # Reusable UI components (GanttChart, ProcessTable, etc.)
│   ├── pages/           # Top-level pages (Results, Compare, Generate)
│   ├── utils/           # API service and helper functions
│   ├── App.js           # Root React component
│   └── index.js         # Entry point and router setup
└── tailwind.config.js   # Tailwind CSS configuration
```

---

## Features

* **Six Scheduling Algorithms**

  * First-Come, First-Served (FCFS)
  * Shortest Job First (SJF)
  * Shortest Remaining Time First (SRTF)
  * Priority Scheduling
  * Round Robin (RR)
  * Priority with Round Robin
* **Interactive Gantt Charts**
  Real-time visualization of process execution timelines.
* **Performance Metrics**

  * Average Turnaround Time
  * Average Waiting Time
  * CPU Utilization
* **Flexible Input Methods**

  * CSV file upload
  * Manual process entry
  * Random process generation with custom parameter ranges
* **Algorithm Comparison**
  Side-by-side metric comparison across all algorithms.

---

## Technologies Used

### Backend

* **Python 3.8+**
* **Flask** for RESTful API endpoints
* **Flask-CORS** to enable cross-origin requests from the frontend

### Frontend

* **React** for building dynamic UIs
* **React Router** for client-side routing
* **Recharts** for chart visualizations
* **Tailwind CSS** for styling
* **Axios** for HTTP requests

---

## Installation

### Backend Setup

1. **Clone the repository** and navigate to the `backend` folder:

   ```bash
   git clone <repo-url>
   cd backend
   ```

2. **Create a virtual environment** (recommended):

   ```bash
   python -m venv venv
   source venv/bin/activate    # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   ```

4. **Run the API server**:

   ```bash
   python api.py
   ```

   The server will be available at `http://localhost:5001/`.

### Frontend Setup

1. **Navigate** to the `frontend` directory:

   ```bash
   cd ../frontend
   ```

2. **Install npm packages**:

   ```bash
   npm install
   ```

3. **Start the development server**:

   ```bash
   npm start
   ```

   The app will open in your default browser at `http://localhost:3000/`.

---

## Usage

### Generate Processes

* Go to the **Generate Processes** page.
* Choose one of:

  * **Random Generation**: specify number of processes and ranges for arrival time, burst time, and priority.
  * **CSV Upload**: upload a file with columns `pid, arrival_time, burst_time, priority`.

### Run a Simulation

* Select a scheduling algorithm from the dropdown.
* For Round Robin or Priority+RR, set the time quantum.
* Click **Run Simulation** to view the Gantt chart and metrics.

### View Results

* The **Results** page displays:

  * An interactive Gantt chart of process execution.
  * A table of each process’s start, finish, waiting, and turnaround times.
  * Overall metrics: average turnaround, average waiting, and CPU utilization.

### Compare Algorithms

* Navigate to the **Compare Algorithms** page.
* Metrics for all six algorithms are displayed side by side, highlighting the best performer.

---

## API Reference

| Endpoint                                   | Method | Description                                       |
| ------------------------------------------ | ------ | ------------------------------------------------- |
| `/api/processes`                           | POST   | Generate random processes and return job ID       |
| `/api/results?job={jobId}&algorithm={alg}` | GET    | Retrieve Gantt log and metrics for one alg.       |
| `/api/compare?job={jobId}`                 | GET    | Compare all algorithms on specified or latest job |

### Request/Response Examples

#### Generate Processes

```json
POST /api/processes
{
  "num_processes": 5,
  "arrival_time_range": [0, 50],
  "burst_time_range": [1, 20],
  "priority_range": [1, 10]
}
```

**Response**:

```json
{ "jobId": "123e4567-e89b-12d3-a456-426614174000" }
```

#### Get Results

```
GET /api/results?job=123e4567-e89b-12d3-a456-426614174000&algorithm=rr&quantum=2
```

**Response**:

```json
{
  "logs": [ { "pid": 1, "start": 0, "end": 2, ... }, ... ],
  "avg_turnaround": 12.5,
  "avg_waiting": 8.2,
  "cpu_util": 0.92
}
```

---

## Contributing

Contributions are welcome! Please:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/YourFeature`).
3. Commit your changes and push to your branch.
4. Open a pull request describing your changes.

---

## License

This project is licensed under the [MIT License](LICENSE).

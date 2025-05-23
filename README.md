# CPU Usage Monitoring with Python and Grafana in Google Colab

This project demonstrates a simple, small, and effective way to monitor CPU usage using Python in Google Colab, store the data in InfluxDB Cloud, and visualize it in Grafana Cloud.

<img src="https://github.com/PlayfulDevBit/Grafana-influx/blob/main/Grafana.jpg" alt="Grafana" width="500" height="300">

## Features
- Collects CPU usage data every 5 seconds using the `psutil` library.
- Stores data in InfluxDB Cloud (free tier).
- Visualizes CPU usage as a time-series graph in Grafana Cloud (free tier).
- Runs entirely in Google Colab, requiring no local setup.

## Prerequisites
- **Google Colab**: Access at [colab.research.google.com](https://colab.research.google.com).
- **InfluxDB Cloud Account**: Free tier at [cloud2.influxdata.com](https://cloud2.influxdata.com).
- **Grafana Cloud Account**: Free tier at [grafana.com](https://grafana.com).

## Setup Instructions

### 1. Set Up InfluxDB Cloud
1. Sign up for a free account at [InfluxDB Cloud](https://cloud2.influxdata.com).
2. Create a bucket named `cpu_metrics`.
3. Generate an API token and note the following:
   - **API Token**
   - **Organization ID**
   - **Bucket Name** (`cpu_metrics`)
   - **InfluxDB URL** (e.g., `https://us-east-1-1.aws.cloud2.influxdata.com`)

### 2. Set Up Grafana Cloud
1. Sign up for a free account at [Grafana Cloud](https://grafana.com).
2. Create a new Grafana instance.
3. Add an InfluxDB data source:
   - Navigate to **Connections > Data Sources > InfluxDB**.
   - Enter your InfluxDB Cloud URL, API token, and bucket name (`cpu_metrics`).

### 3. Run the Project in Google Colab
1. Open [Google Colab](https://colab.research.google.com) and create a new notebook.
2. Install Dependencies
```python
!pip install psutil influxdb-client
```
3. Copy and paste the python code into separate cells.

### 4. Visualize in Grafana
* Create a new dashboard,  Navigate to Dashboards > New Dashboard.
* Click Add a new panel.
* Configure the panel: Select your InfluxDB data source from the Data source dropdown.
* In the query editor, use the following Flux query to retrieve CPU usage data
```
from(bucket: "cpu_metrics")
  |> range(start: -15m)
  |> filter(fn: (r) => r._measurement == "system_metrics")
  |> filter(fn: (r) => r._field == "cpu_usage")
```


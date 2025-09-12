# Assignment #1: Docker Containers

## 📌 Project Overview
The purpose of this assignment is to build and run a simple two-container stack using
Docker and Docker Compose. One container will run a PostgreSQL database, while the other
will host a lightweight Python application. The Python app will connect to the database,
query a few rows, compute basic statistics, and then print and save the results.

---

## What the Stack Does

This project sets up a two-container stack using Docker Compose. One container runs a PostgreSQL database preloaded with trip data, while the other container runs a Python application that connects to the database, queries the data, computes simple statistics, and writes the results to a JSON file. The project demonstrates multi-container orchestration, environment variable configuration, and reproducible workflows.  


## Commands to Run / Stop
### Build and start the stack:
```bash
docker compose up --build
```
###  Stop and remove containers, networks, and volumes:

```bash
docker compose down -v
```


### Using the provided Makefile:
```bash
make        # cleans, builds, and runs everything
make down   # stops and removes containers
```

---

## Example Output

### Stdout (printed by app):
```bash
{
  "total_trips": 6,
  "avg_fare_by_city": [
    {"city": "Charlotte", "avg_fare": 16.25},
    {"city": "New York", "avg_fare": 19.0},
    {"city": "San Francisco", "avg_fare": 20.25}
  ],
  "top_by_minutes": [
    {"city": "San Francisco", "minutes": 28, "fare": 29.3},
    {"city": "New York", "minutes": 26, "fare": 27.1},
    {"city": "Charlotte", "minutes": 21, "fare": 20.0},
    {"city": "Charlotte", "minutes": 12, "fare": 12.5},
    {"city": "San Francisco", "minutes": 11, "fare": 11.2},
    {"city": "New York", "minutes": 9, "fare": 10.9}
  ]
}

```

## Output Location

### Results are written to:
```bash
out/summary.json
```

### Example file content:
```bash
{
  "total_trips": 6,
  "avg_fare_by_city": [...],
  "top_by_minutes": [...]
}
```
## Troubleshooting

Database not ready:
If the Python app starts before Postgres is fully initialized, you may see connection errors. Run again, or ensure the health check in compose.yml is properly configured.

Permission issues on out/ directory:
Make sure the out/ folder exists locally and has the right permissions. You can reset it with:
```bash
rm -rf out && mkdir -p out
```

Port 5432 already in use:
Stop any local Postgres service running on your machine, or change the port mapping in compose.yml.

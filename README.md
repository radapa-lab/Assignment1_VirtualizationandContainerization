Project Overview
This project builds and runs a two-container Docker stack using Docker Compose:
•	A PostgreSQL database container initialized with a trips table and sample data.
•	A Python application container that connects to the database, runs SQL queries, computes simple statistics, prints the results to the terminal, and writes the output to a JSON file.
The purpose of this assignment was to understand how multiple containers can work together using Docker Compose.

What the Application Does
When the stack runs:
1.	PostgreSQL starts and initializes the database using init.sql.
2.	The Python application waits until the database is ready.
3.	The application connects to the database and runs:
o	Total number of trips
o	Average fare grouped by city
o	Top N trips by longest duration
4.	The results are:
o	Printed to the terminal
o	Saved to out/summary.json

How to Run the Project
Make sure you are inside the project root folder.
Build and run the containers:
docker compose up --build
This command:
•	Builds both Docker images
•	Starts the PostgreSQL database
•	Runs the Python application
•	Prints the JSON summary
•	Creates out/summary.json

Stop the containers
After the output appears, press:
Ctrl + C
Then run:
docker compose down -v

Example Output (Terminal)
When the application runs successfully, it prints:
=== Summary ===
{
  "total_trips": 6,
  "avg_fare_by_city": [
    {"city": "Charlotte", "avg_fare": 16.25},
    {"city": "New York", "avg_fare": 19.0},
    {"city": "San Francisco", "avg_fare": 20.25}
  ],
  "top_by_minutes": [
    {"city": "San Francisco", "minutes": 28, "fare": 29.3},
    {"city": "New York", "minutes": 26, "fare": 27.1}
  ]
}
The container exits with:
exited with code 0

Output Location
The generated JSON file is written to:
out/summary.json

Troubleshooting
Database not ready:
If you see repeated "Waiting for database..." messages, wait a few seconds. The app retries until PostgreSQL becomes healthy.
Port 5432 already in use:
Make sure no local PostgreSQL instance is running.
Make command not recognized (Windows):
On Windows, make may not be available. In that case, use:
docker compose up --build

This project demonstrates how to build and run a simple multi-container setup using Docker Compose with automatic database initialization and reproducible execution.


# CCS3308-Virtualization and Containers Assignment_01

# Docker Flask + Redis Visit Counter Application

---

## 📦 Deployment Requirements

Before running this application, ensure you have the following installed:

- **Docker** – Required to build and run containers  
  [Install Docker](https://docs.docker.com/get-docker/)  

- **Docker Compose** *(optional)* – For managing the app with a single command  
  [Install Docker Compose](https://docs.docker.com/compose/install/)  

- **Bash Shell** – For running `.sh` scripts (default on Linux/Ubuntu, available on macOS, and Git Bash on Windows)  

---

## 🌍 Application Description

This application is a **web-based visit counter** that demonstrates containerized deployment using **Flask** and **Redis**.

- **Flask (Python):** Provides a simple web interface that displays how many times the homepage has been visited.  
- **Redis:** Acts as the in-memory data store, keeping track of the visit count.  

Each time you refresh the homepage, the counter increments in Redis and the updated number of visits is displayed.

---

## 🔗 Network and Volume Details

- **Docker Network:** `app-network`  
  A custom bridge network enabling communication between containers by name.  

- **Docker Volume:** `redis-data`  
  A named volume ensuring Redis data is persisted. This means visit counts remain available even if the containers are stopped or restarted.  

---

## ⚙️ Container Configuration

| Container Name | Role           | Port (Host) | Configuration Details                                                                 |
|----------------|----------------|-------------|---------------------------------------------------------------------------------------|
| `redis_db`     | Redis database | `6379`      | Runs Redis with persistence (`--appendonly yes`), data stored in volume `redis-data`. |
| `flask_app`    | Flask web app  | `5000`      | Built from `./app` folder, connects to Redis using environment variable `REDIS_HOST`. |

---

## 🗂️ Container List

- **redis_db** → Stores persistent data (visit counter).  
- **flask_app** → Hosts the Flask application and handles user web requests.  

---

## 🚀 Instructions

### 🔧 How to Prepare the Application

To set up the environment (build image, create volume and network), run:

```bash
./prepare-app.sh

# Step 1: Prepare the application
./prepare-app.sh
Preparing app ...

# Step 2: Run the application
./start-app.sh
Running app ...
The app is available at http://localhost:5000

# Step 3: Open your browser and access the application
# URL: http://localhost:5000

# Step 4: Pause the application (stops containers, keeps data)
./stop-app.sh
Stopping app ...

# Step 5: Delete all application resources (including data)
./remove-app.sh
Removed app.


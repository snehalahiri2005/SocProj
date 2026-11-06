# 🛡️ Real-Time SOC Dashboard – Intrusion Detection & Response System

### Cybersecurity Monitoring | Flask | Python | Docker | Jenkins | CI/CD

A Flask-based Security Operations Center (SOC) dashboard designed to simulate cyberattacks, monitor suspicious login activities, classify threats, and demonstrate automated incident response with Docker and Jenkins CI/CD integration.

[![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-Backend-black?logo=flask)](https://flask.palletsprojects.com/)
[![Docker](https://img.shields.io/badge/Docker-Containerization-blue?logo=docker)](https://www.docker.com/)
[![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-red?logo=jenkins)](https://www.jenkins.io/)
[![GitHub](https://img.shields.io/badge/GitHub-Version%20Control-black?logo=github)](https://github.com/)

---

## 📌 Overview

The **Real-Time SOC Dashboard** is a cybersecurity monitoring and intrusion detection project that provides a centralized interface for monitoring suspicious login activities and simulated cyberattacks.

The application uses Python and Flask for backend processing and HTML, CSS, and JavaScript for the interactive dashboard. It simulates attack scenarios, tracks failed authentication attempts, monitors suspicious IP addresses, and classifies threats into different severity levels.

The system also implements temporary IP and user blocking, attack logging, security notifications, and visual threat monitoring.

To demonstrate DevSecOps practices, the application integrates Docker for containerization, Jenkins for CI/CD automation, and GitHub for source code management.

## ✨ Features

### 1. Real-Time SOC Dashboard
- Interactive security monitoring interface.
- Displays successful and failed login attempts.
- Tracks blocked IP addresses.
- Identifies top attacker IP addresses.
- Displays attack timelines and monitoring statistics.
- Provides automatic dashboard refresh.

### 2. Cyberattack Simulation
The application provides an attacker control panel with options for:
- Brute Force Attacks
- Password Spraying
- Credential Stuffing

Users can select an attack scenario and specify the number of simulated attempts.

### 3. Threat Detection and Classification

The application monitors repeated failed login attempts and classifies suspicious activities using threshold-based detection logic.

| Failed Attempts (within 60 seconds) | Threat Level | Action |
|---|---|---|
| 1–3 | LOW | LOG |
| 4–5 | MEDIUM | WARN |
| 6–8 | HIGH | BLOCK IP |
| More than 8 | CRITICAL | BLOCK USER |

### 4. Automated Response Mechanism
- Temporarily blocks suspicious IP addresses.
- Temporarily blocks targeted user accounts.
- Maintains attack logs and monitoring information.
- Automatically expires temporary blocks.

### 5. Email Alert Notifications
- Uses Flask-Mail and Gmail SMTP.
- Sends security alert notifications for suspicious activities.
- Generates alerts when the failed-attempt threshold is reached.

### 6. Attack Visualization
- Attack timeline using Chart.js.
- Success-versus-failure analysis.
- Top attacker visualization.
- Threat distribution charts.
- Global attack map using Leaflet and OpenStreetMap.
- Searchable live attack logs.

### 7. DevSecOps Integration
- GitHub for version control.
- Jenkins for automated build and deployment.
- Docker for containerization.
- Docker Compose for application execution.
- Jenkins pipeline for building Docker images and replacing running containers.

---

## 🛠️ Technology Stack

| Component | Technology |
|---|---|
| Programming Language | Python |
| Backend Framework | Flask |
| Frontend | HTML, CSS, JavaScript |
| Data Visualization | Chart.js |
| Map Visualization | Leaflet, OpenStreetMap |
| HTTP Requests | Requests |
| Email Notifications | Flask-Mail, Gmail SMTP |
| Version Control | Git, GitHub |
| CI/CD Automation | Jenkins |
| Containerization | Docker |
| Container Management | Docker Compose |

---

## 🏗️ Project Architecture

The application follows a client-server architecture with separate application, attack simulation, and DevOps components.

```text
                 USER / SOC ADMIN
                        |
                        v
              SOC DASHBOARD (HTML/CSS)
                        |
                        v
                FLASK BACKEND
                        |
          +-------------+-------------+
          |             |             |
          v             v             v
      Login API     Attack API     Logs API
          |             |             |
          +-------------+-------------+
                        |
                        v
             THREAT DETECTION ENGINE
                        |
              +---------+---------+
              |         |         |
              v         v         v
             LOW      MEDIUM    HIGH/CRITICAL
              |         |         |
              v         v         v
             LOG      WARN    IP / USER BLOCK
                                  |
                                  v
                            EMAIL ALERTS

              DEVSECOPS PIPELINE
                        |
                  GitHub Repository
                        |
                        v
                     Jenkins
                        |
                        v
                  Docker Build
                        |
                        v
                 Docker Container
                        |
                        v
                 Running Flask App
```

---

## 📂 Repository Structure

```text
SocProj/
│
├── app/
│   ├── app.py
│   ├── requirements.txt
│   └── templates/
│       └── soc.html
│
├── attacker/
│   └── attacker.py
│
├── Dockerfile
├── Jenkinsfile
├── docker-compose.yml
└── README.md
```

### Folder Description

- **app/** – Contains the Flask backend, dependencies, and dashboard template.
- **attacker/** – Contains the Python attacker simulation script.
- **Dockerfile** – Defines the application container image.
- **Jenkinsfile** – Defines the CI/CD pipeline stages.
- **docker-compose.yml** – Defines the Docker Compose application service.

---

## ⚙️ Installation and Setup

### Prerequisites

Install the following tools:

- Python 3.10 or later
- Git
- Docker Desktop
- Docker Compose

### Step 1: Clone the Repository

```bash
git clone https://github.com/snehalahiri2005/SocProj.git
```

Navigate into the project:

```bash
cd SocProj
```

### Step 2: Create a Virtual Environment

```bash
python -m venv venv
```

Activate the environment on Windows:

```bash
venv\Scripts\activate
```

For Linux/macOS:

```bash
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r app/requirements.txt
```

The Flask-Mail dependency must also be included in `app/requirements.txt` because the backend imports Flask-Mail.

### Step 4: Configure Email

Configure Gmail SMTP using environment variables.

Do not hardcode Gmail passwords or application passwords in the source code. The Flask mail configuration should read credentials from environment variables.

### Step 5: Run the Flask Application

```bash
cd app
python app.py
```

Open your browser:

```text
http://localhost:5000
```

---

## 🐳 Docker Deployment

The project includes a Dockerfile that uses Python 3.10, installs the application dependencies, exposes port 5000, and starts the Flask application.

### Build Docker Image

Run from the repository root:

```bash
docker build -t soc-app .
```

### Run Docker Container

```bash
docker run -d -p 5000:5000 --name soc-container soc-app
```

### Access the Application

```text
http://localhost:5000
```

### Using Docker Compose

Build and start the application:

```bash
docker compose up --build -d
```

Stop the application:

```bash
docker compose down
```

---

## 🔄 Jenkins CI/CD Pipeline

The project uses Jenkins to automate the Docker-based deployment workflow.

The Jenkins pipeline consists of the following stages:

| Stage | Description |
|---|---|
| Clone Repository | Fetches the latest source code from GitHub. |
| Build Docker Image | Builds the application Docker image. |
| Stop Old Container | Stops the previously running container. |
| Remove Old Container | Removes the previous container. |
| Run New Container | Starts the updated application container. |

### CI/CD Workflow

```text
Developer
    |
    v
GitHub Push
    |
    v
Jenkins Pipeline
    |
    v
Clone Repository
    |
    v
Build Docker Image
    |
    v
Stop Old Container
    |
    v
Remove Old Container
    |
    v
Run New Container
    |
    v
Updated SOC Dashboard
```

**Note:** The current Jenkinsfile uses Windows `bat` commands, so the configured Jenkins agent must support Windows batch execution and have Docker available.

---

## 📊 Threat Detection Logic

The backend maintains in-memory records of:

- Failed login attempts
- Blocked IP addresses
- Blocked users
- Attack logs
- Attack timelines

The application evaluates failed attempts within a 60-second window.

Based on the attempt count, it assigns a severity level and performs the corresponding action.

Temporary blocking durations:
- IP blocking: 60 seconds.
- User blocking: 120 seconds.

---

## 🔐 Security Considerations

- Use environment variables for sensitive credentials.
- Never commit Gmail App Passwords or API keys to GitHub.
- Use authorized environments for attack simulation.
- The current application uses in-memory storage, so logs and block information are not persistent across application restarts.
- The current attack IP addresses and geographic locations are simulated for demonstration purposes.

**Disclaimer:** This project is developed for educational purposes, cybersecurity demonstrations, and authorized testing only. Do not use attack simulation features against systems without permission.

---

## 🚀 Future Enhancements

- Machine learning-based anomaly detection.
- AI-powered threat prediction.
- Persistent database integration.
- Advanced threat intelligence integration.
- Cloud deployment using AWS, Azure, or Google Cloud.
- Kubernetes-based container orchestration.
- Integration with ELK Stack.
- Advanced automated incident response.
- Improved authentication and role-based access control.

---

## 👩‍💻 Project Information

**Project Title:** Design and Implementation of a Real-Time Intrusion Detection and Response System Using CI/CD

**Project Category:** Cybersecurity | DevSecOps | Full Stack Development

**GitHub Repository:**  
https://github.com/snehalahiri2005/SocProj

---

⭐ If you find this project interesting, consider starring the repository!


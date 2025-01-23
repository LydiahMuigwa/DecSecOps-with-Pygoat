# DevSecOps Pipeline for Python Project with GitHub Actions

## Project Overview
This project demonstrates a DevSecOps pipeline implementation for a Python application using GitHub Actions. The pipeline incorporates both **Static Application Security Testing (SAST)** and **Container Image Scanning** to enhance the security posture of the application.

### Tools Used:
- **[Bandit](https://github.com/PyCQA/bandit):** A Python static analysis tool to identify security vulnerabilities in the code.
- **[Docker Scout](https://docs.docker.com/scout/):** A container image scanning tool to identify vulnerabilities in the built Docker images.
- **GitHub Actions:** To automate the CI/CD pipeline and integrate the scanning tools.

### Application Used:
- **[PyGoat](https://github.com/adeyosemanputra/pygoat):** A deliberately vulnerable Python application designed to help developers learn about security issues.

---

## Pipeline Features
### 1. Static Application Security Testing (SAST) with Bandit
- Scans the Python codebase for security vulnerabilities, including hardcoded secrets, improper exception handling, and input validation issues.
- Generates a JSON report with the findings.

### 2. Container Image Scanning with Docker Scout
- Builds a Docker image for the application.
- Scans the image for known vulnerabilities in operating system packages and dependencies.
- Generates detailed vulnerability reports to aid in remediation.

---

## GitHub Actions Workflow
### Workflow Name:
`CI` (Continuous Integration)

### Trigger:
- The pipeline runs on every `push` to the repository.

### Jobs:
#### 1. **SAST Scan**
- **Environment:** `ubuntu-22.04`
- **Steps:**
  1. Checkout the code.
  2. Set up Python environment (version 3.8).
  3. Install Bandit.
  4. Run Bandit scan on the project.
  5. Save the findings as an artifact.

#### 2. **Image Scan**
- **Environment:** `ubuntu-22.04`
- **Steps:**
  1. Checkout the code.
  2. Set up Docker environment.
  3. Build the Docker image for the application.
  4. Install Docker Scout.
  5. Run Docker Scout quickview and CVE scans.
  6. Save the findings as artifacts.

---

## Running the Project Locally
### Prerequisites
- Docker installed on your machine.
- Python 3.8+ installed.
- Git installed.

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/pygoat.git
   cd pygoat
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the application:
   ```bash
   python manage.py runserver
   ```
4. Build the Docker image:
   ```bash
   docker build -t pygoat:latest .
   ```
5. Run Docker Scout scans locally:
   ```bash
   docker scout quickview
   docker scout cves
   ```

---

## Artifacts and Reports
- **Bandit Findings:**
  - Location: `bandit-report.json`
  - Contains identified security issues in Python code.

- **Docker Scout Reports:**
  - `docker-scout-report.json`: General overview of the image scan.
  - `docker-cves-report.json`: Detailed CVE findings in the image.

---

## Conclusion
This project demonstrates the implementation of a security-focused CI pipeline for Python applications. By integrating SAST and container image scanning tools, it ensures that vulnerabilities are identified early in the development lifecycle. This pipeline serves as a foundation for building more secure applications and can be extended to include additional security checks and automation.


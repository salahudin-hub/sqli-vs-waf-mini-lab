# SQL Injection Mitigation with ModSecurity WAF - Master's Thesis Lab Environment

![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?logo=docker)
![ModSecurity](https://img.shields.io/badge/ModSecurity-CRS-FF6D00?logo=modsecurity)
![DVWA](https://img.shields.io/badge/DVWA-Vulnerable%20App-0078D7)

A reproducible Docker-based lab environment for demonstrating SQL injection attack mitigation using ModSecurity Web Application Firewall. Developed as part of a Master's thesis in Computer and Data Sciences.

## 🎯 Research Objective

This project investigates the effectiveness of ModSecurity with OWASP Core Rule Set (CRS) in detecting and blocking SQL injection attacks in a controlled environment.

## 🏗️ Architecture
Internet User → Nginx + ModSecurity WAF (Port 8082/8443) → DVWA Application (Port 8080) → MariaDB Database

text

## 📦 Prerequisites

- Docker Engine 20.10+
- Docker Compose 2.0+
- 4GB RAM minimum
- 10GB free disk space

## 🚀 Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/salahudin-hub/sqli-vs-waf-mini-lab.git
Start the environment

bash
docker-compose up -d
Access the applications

Direct DVWA access (unprotected): http://localhost:8080
WAF-protected access: http://localhost:8082
HTTPS WAF access: https://localhost:8443 (self-signed cert)
DVWA Setup

Default credentials: admin/password
Set security level to "Low" in DVWA Security settings
Click "Create/Reset Database"
🧪 Testing Methodology

SQL Injection Test

Navigate to SQL Injection page in DVWA
Try payload: ' OR '1'='1
Observe results:

Direct access (8080): Attack succeeds
WAF access (8082): Attack blocked (403/connection reset)
Example curl Commands

bash
# Test direct access (should work)
curl "http://localhost:8080/vulnerabilities/sqli/?id=1&Submit=Submit"

# Test WAF protection (should be blocked)
curl "http://localhost:8082/vulnerabilities/sqli/?id=1' OR '1'='1&Submit=Submit"
📊 Expected Results

Baseline (Port 8080): SQL injection attacks succeed
WAF Protected (Port 8082): SQL injection attacks are blocked with:

HTTP 403 Forbidden responses, or
Connection resets (aggressive ModSecurity blocking)
🔍 Monitoring & Logs

View ModSecurity audit logs:

bash
docker-compose logs waf
Check container status:

bash
docker-compose ps
📝 Thesis Context

This lab environment supports the Master's thesis titled: "Simulating and Mitigating SQL Injection Attacks using a Web Application Firewall in a Virtual Lab Environment"

Research Questions

How effectively does ModSecurity with OWASP CRS detect SQL injection attempts?
What is the performance impact of WAF protection on application response times?
How can organizations implement reproducible security testing environments?
Academic Compliance

Department: Computer and Data Sciences (CDS)
Program: Master's Dissertation (M598 - 60 ECTS)
Research Type: Development-Based Research with Empirical Evaluation
🗂️ Project Structure

text
sqlI-vs-waf-mini-lab/
├── docker-compose.yml    # Container orchestration
├── conf/                 # Application configurations
├── modsec/              # ModSecurity custom rules
├── docs/                # Documentation
└── README.md           # This file
📋 Environment Specifications

Component	Version	Purpose
DVWA	latest	Vulnerable web application
ModSecurity	v3.0.14	Web Application Firewall
OWASP CRS	v3.3.4	Security ruleset
Nginx	1.2x	Reverse proxy
MariaDB	10.11	Database
👥 Author

Salahudin Noor Sheikh Ali
Master's Candidate in Computer and Data Sciences
GISMA University of Applied Sciences

📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

🔗 References

ModSecurity Documentation
OWASP CRS Documentation
DVWA GitHub

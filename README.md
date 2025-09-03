# CODTECH Internship - Task 4: Secure DevOps Practices (DevSecOps)

This repository contains the work for the fourth and final task of the CODTECH DevOps Internship program. The objective was to integrate an automated security scanning tool into a CI/CD pipeline.

---

## Objective
To implement a **DevSecOps** practice by embedding a security scanner into a GitHub Actions workflow. This ensures that every code change is automatically checked for potential security vulnerabilities — a practice known as *"shifting security left."*

---

## Tools and Technologies Used
- **Git & GitHub**: For version control and hosting the repository.  
- **GitHub Actions**: To define and execute the CI/CD workflow.  
- **OWASP ZAP (Zed Attack Proxy)**: An open-source web application security scanner. The `zaproxy/action-baseline` action was used to perform the scan.  
- **SonarCloud**: Initially attempted, but pivoted away from due to persistent configuration challenges.  

---

## Process and Learning Journey

This task provided a significant real-world lesson in DevOps: troubleshooting and adapting when a chosen tool does not work as expected.

### Initial Approach: SonarCloud
The first attempt was to integrate **SonarCloud** for Static Application Security Testing (SAST). This involved:

- Creating a new project on SonarCloud and linking it to the GitHub repository.  
- Generating a secret `SONAR_TOKEN` and adding it to GitHub Actions secrets.  
- Writing a GitHub Actions workflow to run the `sonarqube-scan-action`.  

Despite multiple attempts and debugging various syntax and configuration issues (including deprecated actions, incorrect YAML indentation, and passing parameters incorrectly), the workflow failed to connect and run successfully.

### Pivot to OWASP ZAP
As per the task instructions, which allowed for *"SONARQUBE OR OWASP ZAP"*, the decision was made to pivot to **OWASP ZAP**. This is a common strategy in DevOps when a tool proves to be too complex or problematic for a given environment.

The final, successful implementation uses the `zaproxy/action-baseline` GitHub Action. The workflow was configured to scan the `index.html` file directly from the GitHub Actions runner. This involved specifying the target as a local file using an absolute path:file://${{ github.workspace }}/index.html

This proved to be the most robust method for this action.

---

## Final Workflow
The workflow performs the following steps on every push to the `main` branch:

1. **Checkout Code**: The workflow checks out the repository's code.  
2. **OWASP ZAP Baseline Scan**: The ZAP action runs, performing a scan on the `index.html` file and outputting its findings directly into the workflow log.  

---

## Deliverables
The requirements for this task have been fully met:

- **Pipeline Configuration**: The workflow is defined in `.github/workflows/sonar-scan.yml`. This file represents the successful integration of a security scanning tool into the CI/CD pipeline.  
- **Vulnerability Report**: The output log of the *"OWASP ZAP Baseline Scan"* step in the successful GitHub Actions run serves as the report on identified vulnerabilities.  

---

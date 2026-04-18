# Python CI/CD Pipeline with Snyk Security

![CI Pipeline](https://github.com/Mansi9301/python-cicd-pipeline/actions/workflows/ci.yml/badge.svg)

## The Problem
Manual testing and deployment processes are slow, error-prone, and invisible. 
Teams waste hours running the same checks by hand — and security vulnerabilities 
slip through because no one is scanning dependencies consistently.

## The Solution
I built a production-style CI/CD pipeline from scratch that automatically tests, 
validates, and security-scans every single code change — with zero manual intervention.

## What I Built
A Python calculator app wired into two fully independent CI/CD pipelines:
- **GitHub Actions** — cloud-based, triggers on every push automatically
- **Jenkins** — self-hosted inside Docker, replicating an enterprise environment

Every push to main goes through 4 automated stages before it's considered clean.

## Tech Stack
- Python + pytest — application and test layer
- GitHub Actions — cloud CI/CD pipeline
- Jenkins (Docker) — self-hosted enterprise-style pipeline
- Snyk — automated security scanning on every build

## Pipeline Stages
1. **Checkout** — pull latest code into a clean environment
2. **Install dependencies** — set up Python and install packages
3. **Run tests** — execute all 5 automated tests
4. **Snyk security scan** — flag any high severity vulnerabilities

## Results
- 5/5 tests passing on every build
- GitHub Actions pipeline: passing
- Jenkins pipeline: passing
- No high severity vulnerabilities detected by Snyk
- Zero manual steps required after a code push

## How to Run Locally
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pytest test_calculator.py -v
```

## Key Learnings
- How GitHub Actions workflows are structured and triggered
- How to run Jenkins inside Docker as a self-hosted CI server
- How to manage secrets securely across two different pipeline platforms
- How Snyk integrates into a pipeline to catch vulnerabilities automatically
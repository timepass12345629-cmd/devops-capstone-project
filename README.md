# DevOps Capstone Project - Customer Accounts Microservice

[![CI Build](https://github.com/timepass12345629-cmd/devops-capstone-project/actions/workflows/ci-build.yaml/badge.svg)](https://github.com/timepass12345629-cmd/devops-capstone-project/actions/workflows/ci-build.yaml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.9](https://img.shields.io/badge/Python-3.9-green.svg)](https://shields.io/)

This repository contains the completed project for the [**IBM-CD0285EN-SkillsNetwork DevOps Capstone Project**](https://www.coursera.org/learn/devops-capstone-project?specialization=devops-and-software-engineering), which is part of the [**IBM DevOps and Software Engineering Professional Certificate**](https://www.coursera.org/professional-certificates/devops-and-software-engineering).

## Project Overview

In this capstone project, an Account Microservice for an e-commerce platform is developed, tested, secured, containerized, and deployed following modern agile and DevOps practices:
- **Agile Planning & Kanban**: Tracked sprint user stories, story points, and task transitions across three development sprints.
- **RESTful API Lifecycle**: Implemented CREATE, READ, UPDATE, DELETE, and LIST endpoints for customer accounts using Flask and SQLAlchemy.
- **Test-Driven Development (TDD)**: Written automated unit and integration tests using `nosetests` achieving >95% code coverage.
- **Continuous Integration (CI)**: Configured automated GitHub Actions workflows with linting (`flake8`) and test execution.
- **Application Security**: Hardened HTTP security headers with `Flask-Talisman` and enabled `Flask-CORS` policies.
- **Containerization**: Packaged the microservice with a multi-stage, non-root `Dockerfile`.
- **Cloud Orchestration & CD**: Deployed to Kubernetes / OpenShift and automated continuous delivery with Tekton pipelines.

## Project Structure

```text
├── .devcontainer/             # DevContainer configurations
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   └── user-story.md      # User story issue template
│   └── workflows/
│       └── ci-build.yaml      # GitHub Actions CI workflow
├── bin/
│   └── setup.sh               # Environment setup script
├── deploy/
│   ├── deployment.yaml        # Kubernetes Deployment specification
│   └── service.yaml           # Kubernetes Service specification
├── service/                   # Microservice implementation
│   ├── common/                # Error handlers, log handlers, status codes
│   ├── config.py              # Configuration settings
│   ├── models.py              # SQLAlchemy Account models
│   ├── routes.py              # REST API endpoints (CRUDL)
│   └── __init__.py            # Flask app initialization with Talisman & CORS
├── tekton/                    # Tekton pipeline definitions
│   ├── pipeline.yaml          # Tekton CI/CD Pipeline
│   ├── pvc.yaml               # PersistentVolumeClaim definition
│   └── tasks.yaml             # Tekton Tasks definition
├── tests/                     # Test suite
│   ├── factories.py           # Factory-boy data generators
│   ├── test_cli_commands.py   # CLI command test cases
│   ├── test_models.py         # Model unit tests
│   └── test_routes.py         # REST API and security tests
├── Dockerfile                 # Container image configuration
├── Makefile                   # Automation helper targets
├── Procfile                   # Process manager declaration
├── requirements.txt           # Python project dependencies
├── setup.cfg                  # Test runner & linter configuration
└── user-story.md              # Agile user story specification template
```

## REST API Endpoints

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/` | Root service metadata and links |
| `GET` | `/health` | Service health status check |
| `POST` | `/accounts` | Create a new customer account |
| `GET` | `/accounts` | List all registered accounts |
| `GET` | `/accounts/<id>` | Read a specific customer account |
| `PUT` | `/accounts/<id>` | Update an existing customer account |
| `DELETE` | `/accounts/<id>` | Remove a customer account |

## Running the Application Locally

1. **Initialize the Virtual Environment & Dependencies**:
   ```bash
   python3 -m venv ~/venv
   source ~/venv/bin/activate
   pip install -r requirements.txt
   ```

2. **Start the PostgreSQL Service**:
   ```bash
   make db
   ```

3. **Run Linting & Unit Tests**:
   ```bash
   make lint
   nosetests -v --with-spec --spec-color --with-coverage --cover-package=service
   ```

4. **Launch the Service**:
   ```bash
   honcho start
   ```

## License

Copyright (c) 2023, 2024, 2025, 2026 IBM Corporation and contributors. Licensed under the [Apache License, Version 2.0](LICENSE).

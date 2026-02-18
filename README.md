# AI Software Engineer Assignment - Python HTTP Client

## Overview

This repository showcases a basic HTTP client with an integrated OAuth2 token handling mechanism. It includes a test suite designed to highlight and address a specific bug related to token refresh. The emphasis is on demonstrating a clear setup, targeted testing, and a concise, easily reviewable solution.

## Project Structure

├── app/  
│ ├── http_client.py # The HTTP client implementation  
│ └── tokens.py # OAuth2 token management logic  
├── tests/  
│ ├── conftest.py # Pytest configuration file  
│ └── test_http_client.py # Test suite for the HTTP client  
├── requirements.txt # Project dependencies  
├── Dockerfile # Docker configuration for reproducible testing  
├── Explanation.md # Detailed explanation of the bug and its fix  
└── README.md # This file

## Requirements

- Python 3.12+
- pip

## Installation

### Local Setup

Navigate to the project root directory in your terminal and run:

```bash
pip install -r requirements.txt
```

### Run Tests Locally

From the project root:

```bash
pytest -v
```

This runs the full test suite and verifies the OAuth2 behavior and bug fix.

### Run Tests Using Docker

Build the Docker image

```bash
docker build -t ai-assignment .
```

Run the container

```bash
docker run --rm ai-assignment
```

The container automatically runs:

pytest -v

This simulates a clean CI-style environment.

### Notes

- Dependencies are pinned for reproducibility.

- Docker ensures tests run consistently across environments.

- The bug fix is minimal and covered by focused tests.

### Author Checklist

- Tests run locally

- Docker build succeeds

- Tests pass inside Docker

- Explanation.md documents the bug and fix

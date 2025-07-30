# ⚙️ GitHub Actions DevOps Project

This project demonstrates multiple **CI/CD workflows** using **GitHub Actions** to automate tasks such as testing, deployment, scheduled jobs, and multi-environment management.

## 📂 Workflows Overview

- **push-pr.yml**: Runs tests automatically on push or pull requests targeting `main` or `release/**` branches.
- **manual.yml**: Triggered manually to deploy to `staging` or `production`.
- **scheduled.yml**: Executes a scheduled task every Monday at midnight.
- **main.yml**: Basic workflow that runs on push to `main` .
- **actions.yml**: Mix of commands running on Ubuntu VM and inside Docker containers.
- **jobs.yml**: Demonstrates a matrix strategy to test multiple OS and Node.js versions in parallel.

## 🛠️ Technologies Used

- GitHub Actions
- Docker 
- Node.js 
- Ubuntu Runners
- Workflow Dispatch, Schedule, Matrix Strategy

## 📎 Usage

You can reuse or adapt these workflows in your own repositories to:

- Automate testing and deployment processes
- Trigger jobs manually or on a schedule
- Run cross-platform and container-based tasks

> ✅ Feel free to clone or fork this repository to explore GitHub Actions in real-world DevOps scenarios.

Node.js CI/CD Pipeline with PM2

This repository contains a sample Node.js application with a CI/CD pipeline, designed to demonstrate automated build and deployment using Jenkins and GitHub Actions. The application is managed using PM2 in cluster mode for high availability.

Table of Contents
Pipeline Flow
Process Management
Local Setup
CI/CD with GitHub Actions
Requirements
Troubleshooting
Pipeline Flow

The deployment process follows these steps:

Pull the latest code from the repository
Install dependencies using npm ci
Build the application (npm run build)
Sync build files to the deployment directory
Start or reload the application using PM2
Perform a basic health check or version check
Process Management

The application is managed with PM2:

Runs in cluster mode (instances: max) for load balancing
Uses reload mechanism to update instances without downtime
Deploy path is configurable ($DEPLOY_PATH)
Local Setup

To run the application locally:

# Install dependencies
npm install

# Build the application
npm run build

# Start PM2 in cluster mode
pm2 start ecosystem.config.js

# Check the version endpoint
curl http://localhost:3000/version

Endpoints:

/ → Returns a simple success message
/health → Returns application health status
/version → Returns current deployed version
CI/CD with GitHub Actions

This repository includes a GitHub Actions workflow that automatically:

Installs dependencies (npm ci)
Builds the application (npm run build)
Syncs files to the deployment directory
Starts or reloads the application using PM2
Performs a version check to ensure the latest deployment

Notes for GitHub Actions:

Ensure the deployment directory is writable by the runner
For self-hosted runners, use a home directory path (e.g., $HOME/node-app) to avoid permission issues
Requirements
Node.js (v18+ recommended) and npm
PM2 (npm install -g pm2)
Jenkins (optional, if using Jenkins pipeline)
GitHub Actions (optional, if using GitHub workflow)
Application exposes /health and /version endpoints
Troubleshooting
Old version displayed at /version:
Ensure PM2 reloads the latest dist files
Delete old PM2 instances: pm2 delete all
Restart: pm2 start ecosystem.config.js
GitHub Actions permission issues:
Use a writable directory ($HOME/node-app) instead of /var/www
Ensure the runner user has write access
PM2 cluster fails to start:
Check logs: pm2 logs
Verify the application runs locally first

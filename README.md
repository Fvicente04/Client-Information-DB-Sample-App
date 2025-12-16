# Client Information Management System - Cloud Deployment

**Student:** Felipe Vicente
**Student ID:** [Seu número]
**Module:** B8IS124 Cloud Platform Development
**Lecturer:** Derek Mizak
**Assessment:** CA1 - Cloud Application Deployment & Automation Project

## Project Overview

This project deploys a client information management web application on Google Cloud Platform using automated CI/CD pipelines. The application allows users to create, view, and delete client records stored in a PostgreSQL database.

The application code is based on the sample provided in class. This assessment focuses on cloud infrastructure deployment and automation rather than application development.

## GCP Services Used

### 1. App Engine (Compute)
- Hosts the Node.js application
- Runtime: Node.js 22
- Instance Class: F1
- Auto-scaling: 0-2 instances
- Region: europe-west1

**Why chosen:** Fully managed platform with automatic scaling and simple deployment process.

### 2. Cloud SQL (Database)
- PostgreSQL 17.7 database
- Instance Type: db-f1-micro
- Storage: 10GB SSD
- Region: europe-west1

**Why chosen:** Managed database service with automatic backups and easy integration with App Engine.

### 3. Secret Manager (Security)
- Stores database credentials securely
- Secret: DATABASE_URL

**Why chosen:** Eliminates hardcoded credentials and provides secure access during deployment.

## Architecture

The application uses a three-tier architecture:

1. User accesses application via App Engine URL
2. App Engine connects to Cloud SQL via Cloud SQL Proxy
3. Database credentials retrieved from Secret Manager

## Deployment Pipeline

The cloudbuild.yaml file defines the automated deployment:

**Step 1:** Install npm dependencies
**Step 2:** Run database migrations using Cloud SQL Proxy
**Step 3:** Deploy application to App Engine

When code is pushed to GitHub main branch, Cloud Build automatically:
- Downloads dependencies
- Updates database schema
- Deploys new version to App Engine

## Cost Analysis

Estimated monthly costs based on moderate usage (1000 users/day):

| Service | Cost |
|---------|------|
| App Engine | EUR 4.50 |
| Cloud SQL | EUR 15.20 |
| Secret Manager | EUR 0.03 |
| Cloud Build | EUR 0.00 (free tier) |
| Network | EUR 0.60 |
| **Total** | **EUR 20.33** |

## Local Development

1. Clone repository:
\\\
git clone https://github.com/Fvicente04/Client-Information-DB-Sample-App.git
\\\

2. Install dependencies:
\\\
npm install
\\\

3. Set environment variables:
\\\
DATABASE_URL=postgresql://user:pass@localhost:5432/clientdb
\\\

4. Run migrations:
\\\
npm run migrate
\\\

5. Start application:
\\\
npm start
\\\

## Deployment Steps

1. Create Cloud SQL instance
2. Create database and user
3. Store DATABASE_URL in Secret Manager
4. Connect GitHub repository to Cloud Build
5. Create Cloud Build trigger
6. Push code to main branch

## Live Application

URL: https://client-info-felipe-2025.ey.r.appspot.com

## Database Schema

Table: clients
- id (primary key)
- name (required)
- email (required, unique)
- phone (optional)
- createdAt (timestamp)
- updatedAt (timestamp)

## Technology Stack

- Node.js 22
- Express.js 4.21
- PostgreSQL 17
- Sequelize ORM 6.37
- Google Cloud Platform

## Files Structure

- app.yaml - App Engine configuration
- cloudbuild.yaml - CI/CD pipeline
- app.js - Application entry point
- config/ - Database configuration
- models/ - Sequelize models
- migrations/ - Database migrations

## Security

- Database credentials in Secret Manager
- Cloud SQL Proxy for secure connections
- No hardcoded secrets in code
- HTTPS enforced by App Engine

## AI Tools Usage

**Tools Used:**
- Claude AI: Used for debugging Cloud SQL connection strings and improving documentation clarity
- GitHub Copilot: Used for code autocompletion

**Extent:** Approximately 15% assistance in documentation and 5% in code autocompletion. All cloud architecture decisions and deployment configuration completed independently.

## References

Original application: https://github.com/derekmizak/Client-Information-DB-Sample-App
GCP Documentation: https://cloud.google.com/docs

## License

Apache License 2.0

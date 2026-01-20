# Rooflet Deployment

This repository orchestrates the deployment of the Rooflet application using Docker Compose with git submodules for the backend and frontend services.

## Prerequisites

- Docker and Docker Compose
- Git

## Initial Setup

### 1. Clone this repository with submodules

```bash
# Clone with submodules
git clone --recursive <this-repo-url>

# OR if already cloned, initialize submodules
git submodule init
git submodule update
```

### 2. Add Submodules (First Time Setup)

If you haven't added the submodules yet:

```bash
# Add backend submodule
git submodule add https://github.com/rooflet/rooflet-core backend

# Add frontend submodule
git submodule add https://github.com/rooflet/rooflet-ui frontend

# Commit the submodule configuration
git add .gitmodules backend frontend
git commit -m "Add backend and frontend submodules"
```

## Running the Application

### Development/Local

```bash
# Build and start all services
docker-compose up --build

# Or run in detached mode
docker-compose up -d --build
```

The services will be available at:

- Frontend: http://localhost:7002
- Backend API: http://localhost:7001
- MySQL: localhost:7003

### Stop Services

```bash
docker-compose down

# To remove volumes as well
docker-compose down -v
```

## Updating Submodules

To pull the latest changes from the backend and frontend repositories:

```bash
# Update all submodules to latest commit on their tracked branch
git submodule update --remote

# Or update specific submodule
git submodule update --remote backend
git submodule update --remote frontend

# Commit the updated submodule references
git add backend frontend
git commit -m "Update submodules to latest versions"
```

## Working with Submodules

### Making Changes in Submodules

If you need to make changes within a submodule:

```bash
# Navigate to the submodule
cd backend  # or frontend

# Create a branch and make changes
git checkout -b feature/my-feature
# ... make changes ...
git add .
git commit -m "My changes"

# Push to the submodule's remote
git push origin feature/my-feature

# Go back to deployment repo and update reference
cd ..
git add backend
git commit -m "Update backend submodule reference"
```

# Full Stack Docker Application

A complete full-stack web application demonstrating CI/CD pipeline integration with Docker containerization, load balancing, and automated deployment.

## Tools & Technologies

- **Backend**: NestJS (TypeScript)
- **Frontend**: React with Vite
- **Containerization**: Docker & Docker Compose
- **Reverse Proxy & Load Balancer**: Nginx
- **CI/CD**: GitHub Actions
- **Container Registry**: Docker Hub

## Project Purpose

This project demonstrates a complete CI/CD pipeline for a full-stack application (CSC 424 coursework). It showcases:
- Multi-container application architecture
- Automated build and deployment workflows
- Load balancing with multiple backend instances
- Docker image versioning and tagging

## Key Achievements

- **Built a full CI/CD pipeline from scratch**: Used Multipass as the development + deployment environment, containerized the entire stack, created Docker Hub repos, added GitHub secrets, and automated image building/pushing for frontend, backend, and nginx.

- **Standardized and productionized the stack**: Added a proper nginx Dockerfile, updated docker-compose.yml, removed dev-only mounts, and ensured all services build cleanly and reproducibly across Multipass and GitHub Actions.

- **Implemented automated deployment (CD)**: Created a dedicated deploy workflow, pulled SHA-tagged images into Multipass, and launched a clean production environment using a separate deploy/ compose file.

- **Scaled the backend with load balancing**: Added a second backend container, updated nginx with an upstream block, and verified round-robin balancing using custom headers (X-Served-By).

- **Validated the entire pipeline end-to-end**: Confirmed CI builds, CD deployments, Docker Hub image updates, Multipass-based production runs, and load-balanced traffic — resulting in a fully automated, scalable, production-ready workflow.

## Running the Application

### Local Development

**Backend** (Terminal 1):
```bash
cd backend
npm install
npm run start:dev  # Runs on http://localhost:3001
```

**Frontend** (Terminal 2):
```bash
cd frontend
npm install
npm run dev  # Runs on http://localhost:5173
```

### With Docker Compose

```bash
docker compose up -d
```
Access at http://localhost (via Nginx reverse proxy)

### Testing

**Backend Tests**:
```bash
cd backend
npm run test           # Unit tests
npm run test:e2e       # E2E tests
npm run lint           # ESLint
```

**Frontend Tests**:
```bash
cd frontend
npm run lint           # ESLint
```

## CI/CD Pipeline

The GitHub Actions workflow (`.github/workflows/docker-build-push.yml`) automates:

1. **Trigger**: On merged pull requests to `main` branch
2. **Build**: Creates Docker images for frontend, backend, and nginx
3. **Push**: Pushes images to Docker Hub with tags:
   - `latest`
   - Git commit SHA
4. **Deploy**: Automatically deploys to self-hosted runner

**Required Secrets**:
- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

## Project Structure

- **backend/** - NestJS API server
- **frontend/** - React application
- **nginx/** - Reverse proxy & load balancer configuration
- **docker-compose.yml** - Deployment configuration (2 backend instances)

## License

Part of CSC 424 (CI/CD Pipelines & Load Balancing) coursework.
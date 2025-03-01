# DevOps

**CI/CD Pipelining and DevOps which Includes the following**

1. Manage source code - GitHub
2. Continuous Integration - GitHub Actions
3. Automated Testing - SonarQube and Trivy file Scan
4. Security Tests - SonarQube and OWASP ZAP
5. Packaging - Docker
6. Package Test - Trivy Artifact scan
7. Deployment - Kubernetes and Terraform
8. Monitoring & Logging - Prometheus, ELK Stack, Grafana
9. Feedback Loop - Clickup or Taiga ( Self Host )

## 1.Github

> Have a Github Repo, for managing source code

## 2. GitHub Actions

> Use github Actions to automatically perform a task on certain action

Docs [GitHub Actions]([https://](https://docs.github.com/en/actions)https://)

Get started by Automatically adding a workflow from your Repository, then go to Actions tab. And choose your specific workflow.

Or create file `.github\workflows\[name].yml`

Example YML Code for a simple next.js goes like this.

> I will check deploy on every PR created

Code

```
name: Test Deployment

on:
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    container:
      image: node:20
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 20
      - run: npm install
      - run: npm run build

```

## 5. Docker

> Docker is used to package your app, so that it can run anywhere.

1. First Install Docker from their website according to your system.
2. No need to install any package, the desktop app is all that you want.
3. Run `docker --version` to check if it is working You need to restart your system.
4. run `docker init` in the root directory of your app. Then follow the commands
5. Or Manually create `Dockerfile` ( Without extension ) and paste this code for a simple next.js app, using npm

   ```
   # Use the official Node.js image
   FROM node:20

   # Set the working directory inside the container
   WORKDIR /app

   # Copy package.json and package-lock.json before installing dependencies
   COPY package.json package-lock.json ./

   # Install dependencies
   RUN npm install

   # Copy the rest of the application files
   COPY . .

   # Build the Next.js application
   RUN npm run build

   # Expose the port the app runs on
   EXPOSE 3000

   # Run the Next.js app
   CMD ["npm", "run", "start"]

   ```
6. Then use command `docker build -t [name] .` to build docker file. Which after success, can see in Desktop app.
7. Or use `docker compose up --build` if you initiated using `docker init`

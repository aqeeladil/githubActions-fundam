# Github Actions

GitHub Actions is GitHub's own CICD platform, allowing you to automate workflows directly from your GitHub repository. 

## Key Features

1. **Workflows:** 
- A workflow is an automated process defined in a YAML file in the ```.github/workflows``` directory of your repository. 
- Each workflow can have multiple jobs and triggers based on events like pushes, pull requests, or schedule.
2. **Events:** 
- Events are specific activities in the repository (like push, pull_request, issue, or schedule) that trigger workflows.
3. **Jobs:** 
- Jobs are individual tasks within a workflow that run on GitHub’s virtual environments (runners). 
- Each job in a workflow runs in its own virtual machine or container. 
- Jobs can be run sequentially or in parallel, and they can depend on the completion of other jobs.
4. **Runners:** 
- A runner is a server that runs the steps in a job. 
- GitHub provides hosted runners with pre-configured environments, or you can use self-hosted runners for more control. 
5. **Steps:** 
- Each job consists of multiple steps, which are individual tasks that execute commands in the runner environment. Steps can use either shell commands or actions.
6. **Actions:** 
- Actions are reusable units of code within workflows that perform a specific task and that can be shared across workflows.
- GitHub Actions provides a marketplace with many pre-built actions, where developers can create/publish custom actions and discover actions created by others.
7. **Storing Secrets:** 
- GitHub Actions includes secure storage for sensitive information, such as API tokens, database credentials, or Kubernetes configurations (kubeconfig files).
- These secrets can be accessed during workflow execution without compromising security.

## Workflow:

**Basic Setup:**
- For a Python application, you start by defining a workflow using YAML.
- Use the ```setup-python``` action to configure a Python environment.
- Install required dependencies (e.g., pip, pytest).
- Write and run your test scripts directly within the workflow file.

**Example-1:**
```yaml
name: Example Workflow

on: [push, pull_request] # Events triggering this workflow

jobs:
  build:
    runs-on: ubuntu-latest # Environment to run job

    steps:
      - name: Checkout code
        uses: actions/checkout@v2 # Action to check out code

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

**Example-2:**
- On every push to the main branch, this workflow runsand installs dependencies, runs tests, and builds the project.
```yaml 
name: CI Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

      - name: Build project
        run: npm run build
```

## Jenkins vs Github-Actions

- **Setup:** Jenkins is self-hosted, meaning it requires its own server to run; GitHub Actions is cloud-based and integrated directly into GitHub.
- **Integration:** Jenkins supports multiple version-control systems and can integrate with a wide range of tools and services; GitHub Actions is tightly  integrated with GitHub and so transitioning to another platform (e.g., AWS CodeCommit, Azure DevOps) is challenging.
- **User interface:** Jenkins has a complex and sophisticated user interface, while GitHub Actions has a more streamlined and user-friendly interface that is better suited for simple to moderate automation tasks.
- **Scalability:** Jenkins is highly scalable but self-managed; GitHub Actions scales automatically with GitHub-hosted runners (limited by GitHub’s usage caps).
- **Customization:** Jenkins has extensive plugins for flexibility; GitHub Actions has a growing marketplace but fewer plugins overall.
- **Pipeline as Code:** Jenkins uses Groovy scripts (Jenkinsfile); GitHub Actions uses YAML files.
- **Cost:** Jenkins is free, with costs for hosting infrastructure. It can be expensive to run and maintain, especially for organizations with large and complex automation needs; GitHub Actions, on the other hand, is free for open-source projects and has a tiered pricing model for private repositories, making it more accessible to smaller organizations and individual developers. 

**Use-case:** 
- Jenkins is better suited for complex and large-scale automation tasks. Use Jenkins if you need extensive customization, plugin support, or are working across multiple version control systems. 
- Use GitHub Actions if you’re primarily using GitHub and want a tightly integrated, quick-to-setup CI/CD solution with minimal maintenance. It is a more cost-effective and user-friendly solution for simple to moderate automation needs.

## 
What is Self Hosted Runners ?
Advantages of using Self Hosted Runners ?
Scenario based Interview questions on Self Hosted Runners.
Step by Step Demo to write your first GitHub Actions CI using the Self Hosted Runners. 
EC2 instance as Self Hosted Runners ?

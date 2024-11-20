## Self-Hosted Runners

GitHub Actions supports both default runners and self-hosted runners.

- **Default runners:** Ideal for lightweight tasks and small-scale workflows.
- **Self-hosted runners:** Useful when you need more compute power, security, or want to customize the execution environment (e.g., EC2-Instance, Docker containers, Kubernetes nodes).
- Self-hosted runners allow advanced configurations and are suitable for resource-intensive tasks like load testing.

### Why Use Self-Hosted Runners?

- **Private Projects:** For security-sensitive repositories.
- **Custom Resource Requirements:** E.g., needing 32GB RAM or specific dependencies unavailable in GitHub-Hosted Runners.
- **Enhanced Security:** For sensitive workloads (e.g., banking applications), as the self-hosted environment ensures no external data sharing.

### Advantages of Self-Hosted Runners:

- **Customization:** Tailor the runner's environment to meet project-specific needs.
- **Security:** Ideal for sensitive or proprietary codebases.
- **Cost Efficiency:** Use on-premises resources to save on hosted runner costs for private repositories.

### Example: Configuring a self-hosted runner on an AWS EC2 instance and executing a CI/CD workflow.

1. **Launch an EC2 Instance:**
  - Use Ubuntu as the OS.
  - Configure inbound/outbound traffic rules:
  - Allow only HTTP (port 80) and HTTPS (port 443).
2. **Install and Configure the Runner:**
  - Follow the steps in the ```Settings > Actions > Runners``` section of your GitHub repository.
  - Select "New Self-Hosted Runner" and specify the OS and architecture (e.g., Linux, AMD64).
  - Run the provided commands to download, install, and set up the runner.
  - Execute the ```run.sh``` script on your instance to register it with your GitHub repository.
3. **Modify GitHub Workflow:**
  - Update ```.github/workflows/actions.yml``` to use ```self-hosted``` instead of   ```ubuntu-latest```.
  ```yaml
  name: CI with Self-Hosted Runner

  on:
    push:
      branches:
        - main

  jobs:
    build:
      runs-on: self-hosted
      steps:
        - name: Checkout Code
          uses: actions/checkout@v3

        - name: Run a Script
          run: echo "Hello from Self-Hosted Runner!"
  ```
4. **Test the Setup:**
  - Commit a code change to trigger the workflow.
  - Observe the job being executed on your self-hosted runner via the EC2 instance log


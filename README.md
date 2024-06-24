# GitHub Actions: A Step-by-Step Guide

---
![img](https://github.com/CydexCode/github-actions-demo/assets/112784979/50c4502c-77b9-4740-9245-f0b7a6b7ef2e)


## Introduction

GitHub Actions is a powerful automation platform integrated directly into GitHub repositories, allowing you to automate workflows for building, testing, and deploying your code. This guide covers various aspects of GitHub Actions, including its core concepts and a demo workflow to illustrate how to create, run, and check results.

## Content

1. [What is GitHub Actions](#what-is-github-actions)
2. [Terms: Workflows, Events, Jobs, Steps](#terms-workflows-events-jobs-steps)
3. [How to use GitHub Actions — with step-by-step Demo](#how-to-use-github-actions-with-step-by-step-demo)
4. [Detailed Explanation of demo workflow](#detailed-explanation-of-demo-workflow)

## 1.  What is GitHub Actions

GitHub Actions is a CI/CD (Continuous Integration and Continuous Deployment) service that enables you to automate tasks within your software development lifecycle. With GitHub Actions, you can create custom workflows directly in your GitHub repository, triggered by events such as code pushes, pull requests, or scheduled tasks.

### Key Features:

- **Automation**: Automate repetitive tasks such as building, testing, and deploying code.
- **Integration**: Easily integrate with other services and tools using pre-built actions from the GitHub Marketplace.
- **Customization**: Write custom actions in any programming language or script.
- **Parallel Execution**: Run multiple jobs in parallel to speed up your workflows.
- **Community**: Leverage a vast community of pre-built actions and reusable components.

### Example Use Cases:

- **CI/CD Pipelines**: Automatically build, test, and deploy your applications.
- **Issue Management**: Automatically label issues or close stale issues.
- **Code Quality**: Run static code analysis and linters on every pull request.
- **Notification**: Send notifications to team members via Slack or email when certain events occur.

## 2. Terms: Workflows, Events, Jobs, Steps

### Workflows

In GitHub Actions, a workflow is an automated process set up in a repository to accomplish a specific task, such as CI/CD (Continuous Integration/Continuous Deployment).

**Example:**

```yaml
name: CI

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test 
```

### Events

Events in GitHub Actions are specific triggers that start workflows. These can include pushing code, creating a pull request, scheduling a time, or any other GitHub event.

**Example:**
- push event: Triggers when code is pushed to the repository.
- pull_request event: Triggers when a pull request is opened, synchronized, or reopened.
- schedule event: Triggers at specific times using cron syntax.

```yaml
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  schedule:
    - cron: '0 0 * * *'
```

### Jobs

Jobs are units of work within a workflow. Each job runs in a fresh instance of a virtual environment, and multiple jobs can run in parallel or sequentially depending on their dependencies.

**Example:**

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test

  deploy:
    runs-on: ubuntu-latest
    needs: build  # This job depends on the 'build' job

    steps:
      - uses: actions/checkout@v2
      - name: Deploy
        run: npm run deploy
```

### Steps

Steps are individual tasks within a job. Each step can run commands, use an action, or set up the environment.

**Example:**

- Checkout code: uses: actions/checkout@v2
- Set up Node.js: uses: actions/setup-node@v2
- Run shell commands: run: npm install

```yaml
steps:
  - uses: actions/checkout@v2
  - name: Set up Node.js
    uses: actions/setup-node@v2
    with:
      node-version: '14'
  - name: Install dependencies
    run: npm install
  - name: Run tests
    run: npm test
  - name: Deploy
    run: npm run deploy
```

### Putting It All Together ( Workflow/Events/Jobs/Steps)

Here's a complete example that demonstrates how workflows, events, jobs, and steps are structured in GitHub Actions:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test

  deploy:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - uses: actions/checkout@v2
      - name: Deploy
        run: npm run deploy
```
## 3.  How to use GitHub Actions - with Demo

- To use GitHub Actions, you need to create a workflow file in your GitHub repository. This file defines the events that trigger the workflow, the jobs to run, and the steps within those jobs.

https://github.com/CydexCode/github-actions-demo

### Step-by-Step Demo:

### 1.Create a GitHub Repository

Navigate to GitHub and create a new repository or use an existing one.

![Screenshot 2024-06-24 080358](https://github.com/CydexCode/github-actions-demo/assets/112784979/54f2b5b6-82d6-48b7-a053-a91bad701ccb)

![Screenshot 2024-06-24 080551](https://github.com/CydexCode/github-actions-demo/assets/112784979/93147886-621e-4938-8256-9462af9c952e)

![Screenshot 2024-06-24 080614](https://github.com/CydexCode/github-actions-demo/assets/112784979/b7571f36-cd77-4f4b-a33e-c57a3c7cd233)

### 2. Add a Workflow File:

- Create a .github/workflows directory in your repository.

Click on the “Actions” tab at the top of the page.

![Screenshot 2024-06-24 080749](https://github.com/CydexCode/github-actions-demo/assets/112784979/8151b0ad-4d7e-4186-a395-2ebf23996ea5)

Click the “Set up a workflow yourself” button

![Screenshot 2024-06-24 080900](https://github.com/CydexCode/github-actions-demo/assets/112784979/301adf27-6ff5-4ac2-b3fd-e2b34f3cb9ca)

![Screenshot 2024-06-24 080919](https://github.com/CydexCode/github-actions-demo/assets/112784979/3eedc909-efaf-4533-be4e-b03b917ecb12)

change the yaml file name

![Screenshot 2024-06-24 081024](https://github.com/CydexCode/github-actions-demo/assets/112784979/066d3d34-b1e3-4895-9e0c-ec381aa46880)

### 3. Define the Workflow:

Open the demo.yml file and add the following content:

```yaml
name: demo
on: push
jobs:
  my-job:
    runs-on: ubuntu-latest
    steps:
      - name: my-step
        run: echo "Hello World!"
```

![Screenshot 2024-06-24 083138](https://github.com/CydexCode/github-actions-demo/assets/112784979/bd9042af-fea1-412d-81cb-c38a8090fd35)


### 4. Commit and Push:

Commit and push the demo.yml file to your repository.

![Screenshot 2024-06-24 082100](https://github.com/CydexCode/github-actions-demo/assets/112784979/8c0cd7f8-9fcf-497e-a41d-10ff5a85a121)


![Screenshot 2024-06-24 082120](https://github.com/CydexCode/github-actions-demo/assets/112784979/f7bb8ee9-6638-4491-969a-7956d9404438)

### 5. Check Results:

Navigate to the “Actions” tab in your repository to see the workflow runs. Click on a workflow run to view the details and logs of each step.

![Screenshot 2024-06-24 083332](https://github.com/CydexCode/github-actions-demo/assets/112784979/5fdded59-b0b9-478a-b723-97eca08923ff)

Click on a workflow run to view the details and logs of each step.

![Screenshot 2024-06-24 083710](https://github.com/CydexCode/github-actions-demo/assets/112784979/950cfc97-7bd3-4f65-aac7-029a95e49d2c)

You will see the my-job job and within it, the my-step step displaying "Hello World!".

![Screenshot 2024-06-24 083738](https://github.com/CydexCode/github-actions-demo/assets/112784979/7f96b7b0-2da3-4caa-901b-c0fed11eac13)

![Screenshot 2024-06-24 083809](https://github.com/CydexCode/github-actions-demo/assets/112784979/bec76fb9-783f-4b93-af77-65b963356cfe)

## 4.  Detailed Explanation of Demo Workflow

### Workflow Name and Trigger:

- name: demo: The name of the workflow.
- on: push: The workflow is triggered by a push event to the repository.


### Job Definition:

- jobs: my-job: The workflow contains one job named my-job.
- runs-on: ubuntu-latest: The job runs on the latest version of an Ubuntu virtual environment.

### Steps within the Job:

- steps:: The list of steps to be executed in the job.
- name: my-step: A step named my-step.
- run: echo "Hello World!": The command to be executed in the step, which prints "Hello World!" to the console.


By following these steps and understanding the structure of workflows, events, jobs, and steps, you can start leveraging GitHub Actions to automate and streamline your development workflows effectively.

### ⭐ Support this by Starring Our Repository!

Thank you for your support!
Follow CydexCode on YouTube , TikTok , Linkedin ,GitHub , Facebook , and Telegram for more exciting content! 🎉📱💻📢




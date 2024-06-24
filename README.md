# GitHub Actions : A Step-by-Step Guide

---



Introduction

GitHub Actions is a powerful automation platform integrated directly into GitHub repositories, allowing you to automate workflows for building, testing, and deploying your code. This guide covers various aspects of GitHub Actions, including its core concepts and a demo workflow to illustrate how to create, run, and check results.

Content

What is GitHub Actions
Terms : Workflows , Events , Jobs , Steps
How to use GitHub Actions - with step by step Demo
Detailed Explanation of demo workflow

What is GitHub Actions
GitHub Actions is a CI/CD (Continuous Integration and Continuous Deployment) service that enables you to automate tasks within your software development lifecycle. With GitHub Actions, you can create custom workflows directly in your GitHub repository, triggered by events such as code pushes, pull requests, or scheduled tasks
Key Features:
Automation: Automate repetitive tasks such as building, testing, and deploying code.
Integration: Easily integrate with other services and tools using pre-built actions from the GitHub Marketplace.
Customization: Write custom actions in any programming language or script.
Parallel Execution: Run multiple jobs in parallel to speed up your workflows.
Community: Leverage a vast community of pre-built actions and reusable components.

Example Use Cases:
CI/CD Pipelines: Automatically build, test, and deploy your applications.
Issue Management: Automatically label issues or close stale issues.
Code Quality: Run static code analysis and linters on every pull request.
Notification: Send notifications to team members via Slack or email when certain events occur.

2. Terms: Workflows, Events, Jobs, Steps
Workflows
In GitHub Actions, a workflow is an automated process set up in a repository to accomplish a specific task, such as CI/CD (Continuous Integration/Continuous Deployment).
example:
# yaml
# .github/workflows/ci.yml
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
Events
Events in GitHub Actions are specific triggers that start workflows. These can include pushing code, creating a pull request, scheduling a time, or any other GitHub event.
Examples:
push event: Triggers when code is pushed to the repository.
pull_request event: Triggers when a pull request is opened, synchronized, or reopened.
schedule event: Triggers at specific times using cron syntax.

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  schedule:
    - cron: '0 0 * * *'
Jobs
Jobs are units of work within a workflow. Each job runs in a fresh instance of a virtual environment, and multiple jobs can run in parallel or sequentially depending on their dependencies.
example:
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
Steps
Steps are individual tasks within a job. Each step can run commands, use an action, or set up the environment.
Examples:
Checkout code: uses: actions/checkout@v2
Set up Node.js: uses: actions/setup-node@v2
Run shell commands: run: npm install

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
Putting It All Together ( Workflow/Events/Jobs/Steps)
Here's a complete example that demonstrates how workflows, events, jobs, and steps are structured in GitHub Actions:
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
3. How to use GitHub Actions - with Demo
To use GitHub Actions, you need to create a workflow file in your GitHub repository. This file defines the events that trigger the workflow, the jobs to run, and the steps within those jobs.
https://github.com/CydexCode/github-actions-demo
Step-by-Step Demo:
Create a GitHub Repository

Navigate to GitHub and create a new repository or use an existing one.

2. Add a Workflow File:
Create a .github/workflows directory in your repository.

Click on the "Actions" tab at the top of the page.
Click the "Set up a workflow yourself" button
change the yaml file name
3. Define the Workflow:
Open the demo.yml file and add the following content:

name: demo
on: push
jobs:
  my-job:
    runs-on: ubuntu-latest
    steps:
      - name: my-step
        run: echo "Hello World!"
4. Commit and Push:
Commit and push the demo.yml file to your repository.

5. Check Results:
Navigate to the "Actions" tab in your repository to see the workflow runs. Click on a workflow run to view the details and logs of each step.

click the file
this are the jobs
click the job file
Detailed Explanation of Demo Workflow
Workflow Name and Trigger:
name: demo: The name of the workflow.
on: push: The workflow is triggered by a push event to the repository.

Job Definition:
jobs: my-job: The workflow contains one job named my-job.
runs-on: ubuntu-latest: The job runs on the latest version of an Ubuntu virtual environment.

Steps within the Job:
steps:: The list of steps to be executed in the job.
- name: my-step: A step named my-step.
run: echo "Hello World!": The command to be executed in the step, which prints "Hello World!" to the console.

By following these steps and understanding the structure of workflows, events, jobs, and steps, you can start leveraging GitHub Actions to automate and streamline your development workflows effectively.

---

Thank you for your support!
Follow CydexCode on YouTube , TikTok , Linkedin ,GitHub , Facebook , and Telegram for more exciting content! 🎉📱💻📢

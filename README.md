# DotNet-CICD-Pipeline

## 1. Introduction

This repository demonstrates the basic concepts of Continuous Integration and Continuous Delivery (CI/CD) using GitHub Actions.

The purpose of this project is to understand how to create a workflow, execute commands automatically, and monitor pipeline execution when code is pushed to GitHub.

**Project Level:** Beginner

**Technologies Used:**
- Git and GitHub
- GitHub Actions
- YAML
- Ubuntu Linux Runner

## 2. What Is CI/CD?

### Continuous Integration (CI)

Continuous Integration is the practice of frequently integrating code changes into a shared repository. Automated workflows can build the application and run tests to identify issues early.

### Continuous Delivery/Deployment (CD)

Continuous Delivery automates the process of preparing an application for release. Continuous Deployment goes further by automatically deploying approved changes to the target environment.

## 3. What Is GitHub Actions?

GitHub Actions is a GitHub feature used to automate software development workflows.

It can automate tasks such as:
- Building an application.
- Running unit tests.
- Checking code quality.
- Creating deployment packages.
- Deploying applications to servers or cloud platforms.

Official documentation: https://docs.github.com/en/actions

## 4. Project Structure

```text
DotNet-CICD-Pipeline/
│
├── .github/
│   └── workflows/
│       └── basic-cicd.yml
│
└── README.md
```

### Explanation

- `.github/`: Contains GitHub-specific configuration.
- `workflows/`: Stores GitHub Actions workflow files.
- `basic-cicd.yml`: Defines the workflow, trigger, job, and steps.
- `README.md`: Documents the project.

## 5. Create the Workflow File

Create the following file in your repository:

`.github/workflows/basic-cicd.yml`

Add this code:

```yaml
name: Basic CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: My First Step
        run: echo "This is my first CI/CD pipeline for learning"
```

## 6. Understand Every Line of the YAML File

### 6.1 name

```yaml
name: Basic CI/CD Pipeline
```

Defines the name of the workflow.

This name appears in the **Actions** tab of your GitHub repository.

### 6.2 on

```yaml
on:
  push:
    branches:
      - main
```

Defines the event that triggers the workflow.

- `on`: Specifies when the workflow should execute.
- `push`: Triggers the workflow when code or commits are pushed.
- `branches`: Specifies which branch should trigger the workflow.
- `main`: The workflow runs when a push occurs on the `main` branch.

For example, when you push a change to the `main` branch, GitHub Actions starts the workflow.

Official documentation: https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions

### 6.3 jobs

```yaml
jobs:
  build:
```

A job is a group of steps that execute on a runner.

- `jobs`: Defines one or more jobs in a workflow.
- `build`: The ID of this job. You can choose another valid ID.

A workflow can contain multiple jobs, such as `build`, `test`, and `deploy`.

Official documentation: https://docs.github.com/en/actions/writing-workflows/about-workflows

### 6.4 runs-on

```yaml
runs-on: ubuntu-latest
```

Specifies the runner environment where the job will execute.

A **runner** is a machine that runs your workflow's jobs and commands.

In this example:

- `runs-on`: Specifies which runner environment to use.
- `ubuntu-latest`: Requests a GitHub-hosted runner using the latest Ubuntu image available for the relevant runner label.

Other commonly used runner labels include:

- `ubuntu-latest`: Ubuntu Linux environment.
- `windows-latest`: Windows environment.
- `macos-latest`: macOS environment.

For example, use `windows-latest` if your workflow needs a Windows environment for a particular build or test.

GitHub provides and manages the machine for GitHub-hosted runners. Runner images and preinstalled software can change over time.

Official documentation: https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners

### 6.5 steps

```yaml
steps:
```

Defines the sequence of tasks executed by the job.

Each step performs an action or executes a command.

In this workflow, there are two steps:
1. Checkout repository.
2. My First Step.

Steps in the same job execute sequentially unless execution is affected by conditions or failures.

Official documentation: https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions

### 6.6 name inside a step

```yaml
- name: Checkout repository
```

Provides a readable name for an individual step.

Step names help you understand what is happening in the workflow logs.

For example:
- Checkout repository
- Install dependencies
- Build application
- Run tests
- Deploy application

The hyphen (`-`) indicates an item in a YAML list.

### 6.7 uses

```yaml
uses: actions/checkout@v4
```

The `uses` keyword runs a reusable GitHub Action.

In this example:

- `actions`: The GitHub organization that publishes the action.
- `checkout`: The action used to check out repository code.
- `@v4`: The action version reference.

This action checks out your repository code into the runner's workspace so subsequent steps can access the files.

Without a checkout step, the runner does not automatically have your repository files checked out.

Official documentation: https://github.com/actions/checkout

### 6.8 run

```yaml
- name: My First Step
  run: echo "This is my first CI/CD pipeline for learning"
```

The `run` keyword executes a shell command on the runner.

In this example:

- `name`: Displays the step name in the Actions interface.
- `run`: Executes the specified command.
- `echo`: A shell command that prints text to the console.

Expected output:

```text
This is my first CI/CD pipeline for learning
```

Official documentation: https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions#jobsjob_idstepsrun

## 7. How the Pipeline Works

The workflow follows these steps:

1. A developer makes a code change.
2. The developer pushes the code to the `main` branch.
3. GitHub detects the push event.
4. GitHub Actions starts the workflow.
5. A GitHub-hosted Ubuntu runner is allocated.
6. The checkout action downloads the repository code.
7. The next step executes the `echo` command.
8. The workflow displays the result in the Actions logs.

## 8. How to Run the Pipeline

### Step 1: Create a GitHub Repository

Create a repository named:

`DotNet-CICD-Pipeline`

### Step 2: Create the Workflow Directory

Inside your repository, create:

`.github/workflows/`

### Step 3: Create the YAML File

Create the file:

`basic-cicd.yml`

Place it inside the `workflows` directory.

### Step 4: Add the Workflow Code

Copy the YAML code from Section 5 into the file.

### Step 5: Commit and Push

Commit the file and push it to the `main` branch.

Example commands:

```bash
git add .
git commit -m "Add basic GitHub Actions workflow"
git push origin main
```

### Step 6: Check Workflow Execution

1. Open your GitHub repository.
2. Select the **Actions** tab.
3. Select **Basic CI/CD Pipeline**.
4. Open the latest workflow run.
5. Select the `build` job.
6. Review the output of each step.

A green check mark indicates that the workflow completed successfully.

## 9. Important GitHub Actions Concepts

| Concept | Meaning |
|---|---|
| Workflow | Automated process defined in a YAML file |
| Event | An occurrence that triggers a workflow |
| Job | A group of steps executed on a runner |
| Runner | Machine that executes a job |
| Step | An individual task within a job |
| Action | Reusable functionality invoked using `uses` |
| `run` | Executes a shell command |
| `runs-on` | Selects the runner environment |

## 10. What Have I Learned?

By completing this project, I have learned:

- The basics of CI/CD.
- How GitHub Actions works.
- How to create a workflow using YAML.
- How to configure a push trigger.
- How to define jobs and steps.
- How to select a GitHub-hosted runner.
- How to use `actions/checkout`.
- How to execute shell commands.
- How to monitor workflow execution and logs.

## 11. Limitations of This Project

This is a basic learning project. It does not yet include:

- An ASP.NET Core application build.
- Automated unit testing.
- Code quality checks.
- Docker image creation.
- Environment-specific deployment.
- Production deployment.

These features can be added as the project progresses.

## 12. Next Learning Steps

The next phase will extend this workflow to:

1. Create a basic ASP.NET Core Web API.
2. Install the required .NET SDK on the runner.
3. Restore NuGet dependencies.
4. Build the application.
5. Run automated tests.
6. Publish the application.
7. Add a deployment stage.

## 13. Useful Official Resources

- GitHub Actions: https://docs.github.com/en/actions
- Workflow syntax: https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions
- GitHub-hosted runners: https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners
- Checkout action: https://github.com/actions/checkout
- GitHub Actions quickstart: https://docs.github.com/en/actions/get-started/quickstart

---

**Author:** Waseem Ahmad

**Repository:** DotNet-CICD-Pipeline

**Purpose:** Learning and implementing CI/CD concepts step by step.

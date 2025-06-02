# DevOps-Learning-CI-CD
Repository containing topics I learnt in the CoderCo CICD Module.

## What is CICD?
- CI: Continuous Integration - The practice of automatically integrating code changes from multiple contributors into a shared repository several times a day.
- CD: 
    - Continuous Deployment - Automatically releasing every change that passes all stages of the production pipeline
    - Continuous Delivery - Ensuring the software can be reliably released at any time.
    
## Why is CICD important?
- Faster Delivery: due to automating processes and delivery
- Improved Quality: due to continuously testing and integrating code
- Reduced Risk: due to smaller changes being tested and integrated rather than large changes
- Better Collaboration: Fewer conflicts and better communication

## Github Actions Workflow Syntax and Structure
Must have a workflow file which is a YAML file and is usually located in the .github/workflows. A breakdown of the workflow can be seen below:

![alt text](image.png)

- Events: Actions that trigger workflows (e.g. push, pull request, schedule)
- Jobs: 
    - Independant tasks that run in parallel or sequentially
    - Each job runs on a Virtual Machine
- Steps:
    - Individual commands or actions executed in the job.
    - Steps run sequentially within a job

## Conditions and expressions
- Conditions allow you to control when a job or step should run based on certain criteria
- Expressions provide a way to perform calculations, manipulate strings and more, within your workflow file.

```

# Using Conditions: Run a step only if the previous step succeeded

- name: Run Tests
  run: python -m unittest discover
  if: success()

# Using Expressions: Print a message with the branch name

- name: Print branch name
  run: echo The branch is ${{ github.ref }}

```

## Matrix Builds and Parallel Testing
- Matrix Builds: Allow you to run multiple job configurations in parallel. Useful for testing in different environments such as different OS's

## Secrets and Encrypted Vars
To use secrets, you would need to add it to repository > settings > Add secrets
To use the secret in your workflow file, you would add it as a variable like `${{ secrets.MY_SECRET }}` or if you set it as an environment variable, you can call it with $MY_SECRET

## Creating Custom actions
Reusable units of code which automate specific tasks in your pipeline. There are 3 types of actions; JavaScript actions, docker actions and composite actions which are pieces which are reusable.

To create a custom action:
- Create a new repo for your action
- Define the action metadata in an action.yaml file.
- Write code for your action. This file will be similar to dockerfile if you are writing for docker and index.js for javascript.
- Publish your action to github marketplace (optional)
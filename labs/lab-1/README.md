# 1 Lab1 

Create a new repository on your GitHub account and execute a Github Action workflow with the following details:

- **Repository Name:** hello-world-repo
- **Work on the following branch:** main
- **Workflow File Name:** hello-world.yml
- **Workflow Name:** Hello World
- **Trigger Workflow on:** push events

Workflow specifications:

```yaml
name: Hello World
on: push
jobs:
  hello-job:
    runs-on: ubuntu-latest
    steps:
      - name: Echo text
        run: 'echo "Hello, world!"'
```

The goal is for the workflow to be triggered successfully on push events to the specified branch (main).

# Lab 2

Python Workflow

```yaml
name: CI
'on':
  push: null
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python 3.8
        uses: actions/setup-python@v2
        with:
          python-version: 3.8
      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          
```

# Artifacts-hands-on

**Workflow File:** artifact.yml

**Steps:**

1. Go to the repository and locate the workflow file named `artifact.yml`.
2. Append a new job named - download
    1. This job should execute after the - build job
    2. This jobs runs on - ubuntu-latest
    3. Add step to download the text file from previous job and place it in path: ./artifacts
    4. Add step to display the content of hello.txt file
    5. Use cat ./artifacts/hello.txt command

**Action Steps:**

Append a new job named `download`:

```yaml
name: Workflow Demo
'on':
  - push
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Create a text file
        run: 'echo "Hello, world!" > hello.txt'
      - name: Archive text file
        uses: actions/upload-artifact@v2
        with:
          name: hello-artifact
          path: hello.txt
  download: #added
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Download text file
        uses: actions/download-artifact@v2
        with:
          name: hello-artifact
          path: ./artifacts
      - name: Display content of the text file
        run: cat ./artifacts/hello.txt
```



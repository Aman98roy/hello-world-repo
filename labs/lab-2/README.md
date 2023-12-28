# Exploring Workflow Syntax

**Workflow File:** python-installation.yml

**Steps:**

1. Locate the workflow file named `python-installation.yml`.
2. Go to the "Actions" tab in the repository and click on "I understand my workflows" to enable them.

**Action Steps:**

Update the `build` job:

- Modify the job to include a matrix strategy for the build job/step:
  - Use the `os` key to define operating systems - `ubuntu-latest`, `macos-latest`, `windows-latest`.
  - Use the `py-version` key to define Python versions - `3.7`, `3.8`, `3.9`.
- Revise the "Set up Python" step to make use of these matrix values for installation.

Trigger the workflow by pushing the changes to the repository.

```yaml
name: Installing Python
'on':
  - push
jobs:
  build:
    runs-on: '${{ matrix.os }}'
    strategy:
      matrix:
        os:
          - ubuntu-latest
          - macos-latest
          - windows-latest
        py-version:
          - 3.7
          - 3.8
          - 3.9
    steps:
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '${{ matrix.py-version }}'
          
```

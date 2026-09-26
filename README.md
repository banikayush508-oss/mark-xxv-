name: Run MARK XXV

on: 
  push:
    branches: [ main, master ]
  workflow_dispatch: # Allows you to run it manually from the GitHub app/website

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Set up Python
      uses: actions/setup-python@v5
      with:
        python-version: '3.11'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Install Playwright browsers with dependencies
      run: python -m playwright install --with-deps

    - name: Run MARK XXV main script
      run: python main.py

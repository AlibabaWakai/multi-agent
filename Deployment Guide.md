# Deployment Guide

## 📋 Prerequisites
Before running the code, make sure you have the following set up:

### 📁 Clone the Repository
```bash
git clone https://github.com/viktoriasemaan/multi-agent.git
cd multi-agent/job-hunting-crew
```
> **Git Authentication Error**: remote support for password authentication was removed on August 13 2021**

💡 **Solution 1: Use a Personal Access Token (PAT) for 1-time use- Simplest**
- Go to https://github.com/settings/tokens
- Click "Generate new token" (classic)
- Set expiry date
- No selection of scopes since this is public repo
- Generate token
- Copy token and save it somewhere safe
- When prompted by git clone, use PAT token in place of your password:
- (Optional) If you're on a shared/public computer or want to avoid caching
```bash 
git config --global --unset credential.helper
```

💡 **Solution 2: Developer friendly way**
- using SSH authentication (recommended)- 1 time setup or
- Git Credential Manager (Cross-Platform GUI/CLI Method)

### 🛠 Environment Setup
- Install the required libraries:
```bash
pip install crewai crewai_tools anthropic litellm langchain_community
```

- Ensure Python 3.8+ is installed.
For Ubuntu/Debian (Linux) VMs, 
```bash
python3 --version
```

- Use either
  * **Jupyter Notebook**: Install Jupyter Notebook and open the provided `.ipynb` file.

  * **VS Code (Jupyter Extension)**: Open the `.ipynb` file in Visual Studio Code with the Jupyter extension for an integrated coding experience.

  * **Google Colab**: Upload the `.ipynb` file to Google Colab for an easy-to-use cloud environment.

  * **Amazon SageMaker**: Use Amazon SageMaker Studio for a managed and scalable machine learning environment.

- **(Optional): Use virtual environment (or conda environment)**
> Recommended for Jupyter Notebooks, Python development or reproducible projects. This avoids messing with system Python.

```bash
python3.8 -m venv myenv
source myenv/bin/activate    # Linux/macOS
```

> When your prompt changes from xx-virtual-machine: ~/multi-agent to (myenv) xx-virtual-machine: ~/multi-agent, (myenv) part means your virtual environment named myenv is activated.


📦 Installing Jupyter notebook inside virtual environment
```bash
pip install notebook
```

💡 Note: If the project uses environment variables from a .env file, you may also need to install python-dotenv. In this case, check utils.py.
```bash
nano utils.py
```
> Search for import dotenv or from dotenv import load_dotenv. Since this exist, installation is necessary.

```bash
pip install python-dotenv
```

### 🔑 API Keys
1.**Serper API Key** (or other search APIs):
  * Sign up at [Serper](https://serper.dev) to obtain an API key.
  * Rename sample.env to .env
  * Add the key to the .env file as SERPER_API_KEY.

# Python Environment Configuration with Caching
This repository provides a Python module utils.py for managing environment variables with caching, validation, and default configurations. It's designed to simplify handling environment-specific settings in your Python applications.

**Installation**
No installation is needed since this is just a single Python file. Simply place the utils.py (replace with the actual name of your script) in your project directory.

**Environment Variable Files**
-In job-hunting-crew folder, rename samples.env to .env

```bash
mv sample.env .env
```
💡 Note: .env is a hidden file. To access it, use
```bash
ls -a
```

-update the API keys in those files.


# Freeze dependencies
pip freeze > requirements.txt

# Later or on another machine
pip install -r requirements.txt




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



# Python Environment Configuration with Caching
This repository provides a Python module utils.py for managing environment variables with caching, validation, and default configurations. It's designed to simplify handling environment-specific settings in your Python applications.

**Installation**
No installation is needed since this is just a single Python file. Simply place the utils.py (replace with the actual name of your script) in your project directory.

### Environment Variable Files
### 🔑 API Keys
1.**Serper API Key** (or other search APIs):
  * Sign up at [Serper](https://serper.dev) to obtain an API key.
  * Rename sample.env to .env in job-hunting-crew folder
```bash
mv sample.env .env
```
💡 Note: .env is a hidden file. To access it, use
```bash
ls -a
```
    
  * Add the key to the .env file as SERPER_API_KEY.

https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

### 🔧 AWS Configuration
To use models on Amazon Bedrock, follow these steps:

#### 1. Sign Up for an AWS Account (if you don’t have one)**
* Create a [free-tier](https://aws.amazon.com/free/) AWS account at AWS Free Tier.
* Ensure your account is fully activated before proceeding.
#### 2. Install AWS CLI**
* Download and install the [AWS Command Line Interface (CLI)](https://aws.amazon.com/cli/) from the AWS CLI Installation Guide.
[AWS CLI user guide v2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
* To install the AWS CLI, run the following commands:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
💡 Note: Please refer back to documentation for more details such as updating aws cli commands.

* Verify the installation by running:
```bash
aws --version
```

#### ✅ 3. Step-by-Step: How to Get AWS Access Keys
##### 1. Log in to AWS Console
Go to https://aws.amazon.com/console and sign in with your AWS account.

##### 2. Go to the IAM Management Console
You can directly go here: https://console.aws.amazon.com/iam

##### 3. Access the "Users" section
* In the left sidebar, click on "Users".
* Click on your username (or create a new user if you don’t have one).

##### 4. Create Access Keys
* Go to the "Security credentials" tab.
* Scroll down to Access keys.
* Click "Create access key".
* Select use case: AWS CLI

##### 5. Download or Copy Your Keys
* You will see both:
** Access Key ID
** Secret Access Key

* Important: Save the Secret Access Key somewhere secure. AWS will not show it again.

#### 4. Configure AWS Credentials
Run the following command to set up your AWS credentials:
```bash
aws configure
```
You will be prompted to enter:

* **AWS Access Key ID**
* **AWS Secret Access Key**
* **Default AWS Region** (e.g., us-west-2)
* **Output format** (default is json)
When selecting a region, choose one where Amazon Bedrock models are available. You can check model availability across different AWS regions in the official documentation [Supported Models and Regions](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html). If models are available in multiple regions, select the one closest to you to minimize latency.

💡 How to verify it worked?
Run this command to check your current configured identity:
```bash
aws sts get-caller-identity
```

You should see JSON output showing your AWS account ID and ARN, confirming you’re authenticated.
> If you find that your selected region does not have a variety of models, you can resolve issue

🔁 Option 1: Run aws configure again to overwrite default
If you're okay with just one active region at a time
```bash
aws configure
```

* Re-enter the region only (e.g., us-east-1)
* Just press Enter when asked for Access Key ID and Secret Access Key to reuse existing ones
* Output format? Press Enter for json or your previous value

🔄 Option 2: Use named profiles (Recommended for multi-region setups)
This lets you store multiple region settings, each with its own name:
```bash
aws configure --profile us-east
```
* Set Access Key ID
* Set Secret Access Key
* Set region to us-east-1
Then to use it:
```bash
aws s3 ls --profile us-east
```
You can still keep your original Japan setup as the [default] profile.
✅ This is ideal if you want to test different regions or switch often without redoing your config.

How to Circumvent or Minimize Info Sharing
1. Use Generic or Personal Info
For company name, you can use your own name or a generic “Independent Developer” or “Personal Use”

For URL, use a personal website or LinkedIn page, or a placeholder URL (like https://example.com)

For Industry, pick the closest category or “Individual” / “Other”

Many users do this successfully, especially if using the models for personal projects or prototyping.

# Freeze dependencies
pip freeze > requirements.txt

# Later or on another machine
pip install -r requirements.txt




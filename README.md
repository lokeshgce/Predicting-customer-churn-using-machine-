# Predicting-customer-churn-using-machine-
from github import Github
import os

# --- STEP 1: CONFIGURATION ---
GITHUB_TOKEN = "your_personal_access_token"  # Replace with your actual token
REPO_NAME = "customer-churn-prediction"     # Your new repo name
DESCRIPTION = "Predicting customer churn using machine learning to uncover hidden patterns"

# Path to your local project folder (update if needed)
local_repo_path = "./customer-churn-prediction"

# --- STEP 2: AUTHENTICATE & CREATE REPO ---
g = Github(GITHUB_TOKEN)
user = g.get_user()
repo = user.create_repo(REPO_NAME, description=DESCRIPTION, private=False)

# --- STEP 3: PUSH FILES ---
for root, dirs, files in os.walk(local_repo_path):
    for file in files:
        file_path = os.path.join(root, file)
        with open(file_path, "rb") as f:
            content = f.read()
        remote_path = os.path.relpath(file_path, local_repo_path).replace("\\", "/")
        repo.create_file(remote_path, f"Add {remote_path}", content)

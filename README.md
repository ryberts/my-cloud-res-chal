AWS Cloud Resume Challenge

Step #13 and #14 - Source Control and GitHub Actions CI/CD (Front End) of your Cloud Resume Challenge:

## 📁 Step 13 & 14: Source Control & GitHub Actions CI/CD (Front End)

For this step of the Cloud Resume Challenge, I implemented source control using Git and GitHub, and automated the deployment of my static website to an S3 bucket using GitHub Actions. Below is a summary of my approach, tools used, and configuration steps.

---

### 🧩 Source Control Setup

Repository: [ryberts/my-cloud-res-chal](https://github.com/ryberts/my-cloud-res-chal)

1. Created a new repository in GitHub.
2. On my local PC, I created a working directory:  
   ```powershell
   cd Downloads
   mkdir my-cloud-res-chal-git
   cd my-cloud-res-chal-git
3. Initialized Git and committed files:

git init
git add .
git commit -m "initial commit"
git branch -M main

4. Connected to GitHub and pushed the code:

git remote add origin https://github.com/ryberts/my-cloud-res-chal.git
git push -u origin main

⚙️ GitHub Actions: CI/CD Workflow for Front-End
To automate deployment to AWS S3, I set up a GitHub Actions workflow using jakejarvis/s3-sync-action.

📁 Directory: .github/workflows/upload.yml

name: Upload Website

on:
  workflow_dispatch:
  push:
    branches:
      - main  # Trigger only on pushes to the main branch

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - uses: jakejarvis/s3-sync-action@master
        with:
          args: --acl private --follow-symlinks --delete
        env:
          AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: 'us-east-1'
          SOURCE_DIR: 'my-cloud-res-chal'  # Local directory containing website files


🔐 Secrets (configured in GitHub repo):

AWS_S3_BUCKET

AWS_ACCESS_KEY_ID

AWS_SECRET_ACCESS_KEY

📺 Reference Materials
🎥 Rishab’s Video - <a href="https://www.youtube.com/watch?v=qFEf6iOo-4g">Setting up Git and CI/CD</a>

💡 GitHub Action Used: jakejarvis/s3-sync-action

  

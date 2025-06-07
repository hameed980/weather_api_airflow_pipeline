# How to Push EC2 Code to GitHub Using Git

Run these commands step-by-step to push your EC2 project code to GitHub.

```bash
# STEP 1: On your local machine terminal (Mac/Linux) or Git Bash (Windows), connect to your EC2 instance:
chmod 400 my-key.pem         # Run once, only if not done already
ssh -i my-key.pem ec2-user@<your-ec2-public-ip>    # Replace with your EC2 info; if Ubuntu, use 'ubuntu' instead of 'ec2-user'

# STEP 2: Inside the EC2 terminal, install Git:
# For Amazon Linux:
sudo yum update -y
sudo yum install git -y

# For Ubuntu:
sudo apt update
sudo apt install git -y

# STEP 3: Configure Git with your name and email:
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"

# STEP 4: Generate an SSH key on EC2:
ssh-keygen -t ed25519 -C "your_email@example.com"
# Press Enter 3 times to accept defaults and no passphrase

# STEP 5: Display the public SSH key:
cat ~/.ssh/id_ed25519.pub
# Copy the output starting with ssh-ed25519

# STEP 6: On your local machine browser:
# - Log in to GitHub
# - Go to Settings → SSH and GPG keys
# - Click New SSH key
# - Give it a title (e.g., "EC2 SSH")
# - Paste the copied SSH key
# - Click Add SSH Key

# STEP 7: Back in EC2 terminal, test SSH connection to GitHub:
ssh -T git@github.com
# You should see a message like: Hi your-username! You've successfully authenticated...

# STEP 8: Navigate to your project directory in EC2:
cd /home/ec2-user/myproject/  # Or your actual project folder path

# STEP 9: Initialize git, add remote, commit, and push code to GitHub:
git init
git remote add origin git@github.com:your-username/your-repo.git
git add .
git commit -m "Initial commit from EC2"
git branch -M main
git push -u origin main

# DONE! Your EC2 project code is now pushed to GitHub.

How to Push EC2 Code to GitHub Using Git
🔹 STEP 1: Connect to Your EC2 Instance
🖥️ Run this on your Local Machine Terminal (Mac/Linux) or Git Bash (Windows):

chmod 400 my-key.pem         # Run once, only if not done already
ssh -i my-key.pem ec2-user@<your-ec2-public-ip>
Replace my-key.pem with your actual key file name.
Replace <your-ec2-public-ip> with your EC2 instance’s public IP.
If you're using Ubuntu, replace ec2-user with ubuntu.
✅ You are now inside your EC2 terminal.

🔹 STEP 2: Install Git
🖥️ Run this inside the EC2 Terminal:

For Amazon Linux:
sudo yum update -y
sudo yum install git -y
For Ubuntu:
sudo apt update
sudo apt install git -y
🔹 STEP 3: Configure Git
🖥️ Still inside the EC2 Terminal, run:

git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
🔹 STEP 4: Generate SSH Key
🖥️ Still inside the EC2 Terminal, run:

ssh-keygen -t ed25519 -C "your_email@example.com"
Press Enter 3 times to accept default path, no passphrase.
🔹 STEP 5: Copy the Public SSH Key
🖥️ Still inside the EC2 Terminal, run:

cat ~/.ssh/id_ed25519.pub
Copy the output (starts with ssh-ed25519 ...).
🔹 STEP 6: Add the Key to GitHub
🌐 Run this step in your Browser (on your local machine):

Log in to GitHub.
Go to Settings → SSH and GPG keys.
Click New SSH key.
Give it a title like EC2 SSH.
Paste the key (copied from Step 5).
Click Add SSH Key.
🔹 STEP 7: Test SSH Connection
🖥️ Back to EC2 Terminal, run:

ssh -T git@github.com
Expected output:

Hi your-username! You've successfully authenticated...
🔹 STEP 8: Go to Your Project Directory
🖥️ In EC2 Terminal, navigate to your project folder:

cd /home/ec2-user/myproject/   # Or your actual project folder path
🔹 STEP 9: Push Code to GitHub
If you already created an empty GitHub repo (no README), run in EC2 Terminal:

git init
git remote add origin git@github.com:your-username/your-repo.git
git add .
git commit -m "Initial commit from EC2"
git branch -M main
git push -u origin main

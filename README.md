# Azure:
## Create a VM and install an app using the CLI

## Objective
In this project, I wanted to start using the CLI to perform Azure functions.

## Skills learned
- Creating a VM on Azure (still using the GUI)
- Installing the Azure CLI on Windows and Linux
- Setting permissions for the SSH key
- Installing an app (in this case I installed Jenkins) using the CLI

## Tools used
- Microsoft Azure dashboard
- Linux CLI

## Steps
1. Log in to Az dashboard.
2. Create a new VM with an Ubuntu OS
3. Download the SSH key
4. Make a note of the public IP address!
5. I tried to do the next steps from my Win-11 system by using Git-Bash, but it kept giving errors in the path for the SSH key. I kept getting "path not found". I looked for some advice online, and tried wrapping the path in double quotation marks "" "", but this didn't fix the issue. I then decided to try using the Windows cmd commandline with the Azure CLI installed. This fixed the path issue, but the permissions for the SSH key needed to be set manually, which didn't work. Back to trusty Linux CLI...
6. From my Linux environment, I logged into Azure again, and recreated an SSH key to download. Now I was set.
7. Set the permissions of the SSH key .pem file using chmod 600.
8. Connect to the Azure VM using the following command:
   ssh -i /[SSH key path and filename.pem] azureuser@[Public IP address]
9. Now install Java:
   sudo apt update
   sudo apt install openjdk-17-jre
10. Verify that Java is installed:
   java -version
   The current release of Jenkins requires at least java version 17.
11. Install Jenkins:
    curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
      /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
      https://pkg.jenkins.io/debian binary/ | sudo tee \
      /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    sudo apt-get install jenkins
12. Open the Azure GUI again, and create a new network rule for port 8080 to allow inbound traffic.
13. Voila!

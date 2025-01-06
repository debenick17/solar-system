## Connect GitHub to you EC2 Instance

- Run `cd .ssh`
- Run `ssh-keygen`
- Verify key is generated with `ls`
- Run `cat id_rsa.pub`
- Copy the output of the cat command above
- Go to GitHub settings under your profile and select **SSH and GPG Keys**
- Click New **SSH Key**
- Give the name and paste the key you copied earlier
- Test if everything is fine by typing `ssh git@github.com`

## Connect VScode to your EC2 Instance

- Make sure you have a running AWS EC2 Instance. Also make sure you downloaded the keypair
- Open VSCode locally, go to the Extension section and install `Remote - SSH` from Microsoft
- Once Installed, you should see a new Status bar item at the bottom far left. The status item can be used to quickly open the Remote SSH settings. Click on the status item.

- Select **Open The Configuration file**
- Choose the config file corresponding to the current user
- Now enter the following details, make sure it matches with information from your EC2 Instance

```
Host ec2_instance
    HostName ec2-23-22-108-73.compute-1.amazonaws.com
    User ubuntu
    IdentityFile ~/Downloads/web-server-kp.pem

=======================================================
NOTE:
- Host (aws-ec2) is just a name that will appear in VS Code. It can be any name.
- HostName is the server’s host or IP.
- User is the Ubuntu username.
- IdentityFile is the path to the private key.

```

- Save the configuration file
- Open your terminal to where you downloaded the `.pem` file and grant permissions by running the command `chmod 400 "web-server-kp.pem"` (replace "_web-server-kp.pem_" with the name of your own `.pem` file)
- Click the status item on the bottom left and select **Connect to Host**. You should now be able to see your host

## Setting Up and Executing the Project

- Clone the project on GitHub
- Open the project in the terminal and cd to the project
- Delete the .git folder by running the command `rm -rf .git`
- Go to github and create a repository, name it "**solar-system**"
- Follow the instructions and push an existing repository to newly created repository
- Create a `Dockerfile` in the root directory of the project. Copy the content from [here](https://github.com/debenick17/solar-project/blob/main/Dockerfile)
- Create A `.dockerignore` file in the root directory. Copy the content from [here](https://github.com/debenick17/solar-project/blob/main/.dockerignore)
- Create a folder named ".github". In that folder create another folder "workflows", create a file named `ci.yml` in workflows folder for the GitHub Actions workflows. Copy the content from [here](https://github.com/debenick17/solar-project/blob/main/github/workflows/solar-system.yml) and go through it
- Create the respective environment variable (MONGO_USERNAME with value "superuser") and secret (MONGO_PASSWORD with value "SuperPassword") in your Github Actions. To do that go to your github project repository settings ---> **Security** ---> **Secrets and varaibles** and click on `Actions`
- Save everything then git add, commit and push to the git repository you created
- Go to GitHub and click **Actions** in the project repository to see the actions running

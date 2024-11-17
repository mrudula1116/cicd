#for typing in user data of ec2 instance
sudo apt-get update -y
sudo apt-get install wget curl git vim ca-certificates gnupg lsb-release -y
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update -y
sudo apt-cache policy docker-ce
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
sudo usermod -aG docker <USERNAME>
sudo sudo systemctl start docker
sudo sudo enable start docker
sudo wget https://github.com/docker/compose/releases/download/v2.14.0/docker-compose-linux-x86_64 -O /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
#docker installation with cmd:
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y #adding dependices
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg #adding gpg key of docker
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null #docker apt repo
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
sudo docker --version
sudo docker run hello-world

# Start the Nginx server
CMD ["nginx", "-g", "daemon off;"]
type vi default.conf
paste the below code
server {
        listen 80 default_server;
        root /usr/share/nginx/html;
        index index.html;
        server_name mysite.com;
} hit esc+shift+:wq then enter
#if it says permission denied then hit following commands for docker build -t testimg:v1 . 
groups $USER
sudo usermod -aG docker $USER
ls -l /var/run/docker.sock
sudo chmod 666 /var/run/docker.sock
sudo systemctl restart docker
sudo systemctl status docker
type docker images
#to exit from vi type :w then :q and enter 
type code in vi index.html , vi style.css, vi script.js
then in vi.dockerfile type FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80
in cmd : docker run -d -p 80:80 -v ./site:/usr/share/nginx/html nginx
type docker build -t mysite .
docker run mysite

#remove swp dockerfile as vim -r dockerfile ,  rm -f.dockerfile.swp

#for cicd web devlopment with jenkins,git,local server like nginx
1] create key pair
2]create security group
3]launch instance with allow port 80 and 22 in description , also aloowing tcp,ssh traffic with anywhere ipv4
4] choose existing keypair and security group while launching instance
5]open cmd copy ssh client key and paste it also copy chmod command in connect part of ec2
6]sudo apt-get update
7]sudo apt install openjdk-11-jre
8]java --version
9] $ curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
          $ echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \   https://pkg.jenkins.io/debian binary/ | sudo tee \   /etc/apt/sources.list.d/jenkins.list > /dev/null
          $ sudo apt-get update
          $ sudo apt-get install jenkins
          type above commands individually
10]  $ sudo systemctl enable jenkins
          $ sudo systemctl start jenkins
          $ sudo systemctl status jenkins
11]let's open the default TCP port 8080 under the Security Group of your Instance and allow MYIP only to access the Server.
For security purposes, I hid my IP.

12]copy public ip of ec2 and paste into browser you will see unlock jenkins
13]go to /var/lib/jenkins/secrets/initialAdminPassword get the password enter into page
14]install plugins
15]give credentials such as username , password and an dummy email
16]after continuing wizard will display jenkins url through which we can aceess server then save and finish
17]click on new item enter name , Enter the name of your first item and select Freestyle Project and click on Ok.
18]Now we need to configure various parameters of our first job in Jenkins. Under the General section, put the description of your project. Under Project Url paste the GitHub URL of the project for which we need to create the CI CD Pipeline.
19]Under Source Code Management we need to paste the GitHub repository URL as shown in the below screenshot:
20]Under credentials, we first need to generate the ssh keys on our EC2 Server.
The reason to create ssh keys is to make secure integration between our Jenkins Server and Github and this way we can clone any git repo in this Jenkins instance. You do not need to provide the credentials while configuring the job in Jenkins.
21]Take the public key and insert that under the settings in GitHub to achieve a password-less connection between Jenkins and GitHub.

For that go to the settings of your GitHub, on the left choose SSH and GPG keys, click on New SSH key, give the name under Title, and paste the public key under the Key section we previously generated on the EC2 server.
22]After adding the ssh key to our GitHub account we will add the credentials in Jenkins. For that, under credentials click on Add button and click on Jenkins in the drop-down option.
23]A new window will appear. Select SSH Username with private key under the section Kind. Give any name under section ID and Description, as shown in the below screenshot:
24]On the other half of this page type the Username of the EC2 machine which in our case is ubuntu and then paste the private ssh key copied from your EC2 server and click on Add button.
25]Now we have to specify the branch of our GitHub repository. It can be any branch the developer would have been working on. In our case, we will select the master branch.
26]This is all we need so far as the configuration of our first job is concerned. We can save this part of the configuration and move to the next step of building the project.
27] To check whether our GitHub integration with Jenkins is successful we will do a small test by clicking on Build Now on the left navigation bar in our first job as shown below
28]After clicking on Build Now we see in the output console that the build has been finished successfully and Jenkins was able to fetch the code from our GitHub repository. That means Jenkins Integration with GitHub is successful.
29]To run the code we will go through the steps provided by the developer in the Readme file of the Repo which is as shown below:

sudo apt install nodejs
sudo apt install npm
npm install
node app.js
30]After allowing port 8000 in the inbound policy of Security Group we will run the final command as: then node app.js
31]To check the output open your browser take the public IP of your EC2 Instance with port 8000 and you will see the result as:
32]install docker
33]automate process with jenkins 
type commands in execute shell:
For that go under the Build Steps section of Jenkins configure settings of our job and add the following commands in the execute shell area:
docker build . -t todo-node-app
     docker run -d --name node-todo-app -p 8000:8000 todo-node-app click save
34] Now Click on Build Now to build the job using Jenkins.

After you click on Build Now you may encounter an error in your build as shown in the below screenshot:

35]To solve this run the below commands in the EC2 Server which adds the Jenkins user to the docker group and restarts the Jenkins server.
36]    $ sudo usermod -aG docker jenkins
              $ sudo systemctl restart jenkins
37]After the Jenkins Server restarts, again run the Build Now and check the Output:
38] webhook configure : 
To configure the web hook we first need to kill the docker container running on our EC2 Instance by issuing the docker kill “container-id” command.

After that, we will install the GitHub Integration plugin in our Jenkins Server

Jenkins -> Manage Jenkins -> Manage Plugins -> Install github integration plugin
37]After adding the plugin we need to add the webhook in our GitHub repo as shown in the screenshot:
38]A new window will appear where first add the Payload URL which will be the URL through which you access your Jenkins Server with the addition of github-webhook keyword.
The content type should be application/json, the rest should be kept at default and then click on Add webhook.
39]The green tick before the Payload URL indicates that the webhook has been successfully configured with Jenkins as shown below:


40]Now we need to go to the Configure Settings of our Jenkins first Job and select GitHub hook trigger for GITScm polling under Build Triggers and click on Save.
41]Now we will update something in our GitHub repo and our job should get triggered automatically in Jenkins.

The moment I changed something in the code the build got triggered in our Jenkins Job.
42]If we check the status of our job it shows that the build got started by GitHub push as shown in the below screenshot:

#ci with jenking,git:
To set up a Continuous Integration (CI) process using Jenkins and GitHub, you’ll need to configure Jenkins to build and test your GitHub-hosted project whenever changes are pushed to your repository. Here’s a step-by-step guide:

Prerequisites:

You should have a GitHub repository with your project code.
Jenkins should be installed and configured on a server.
Steps:
Install Jenkins GitHub Plugin:

Log in to your Jenkins server.
Go to “Manage Jenkins” > “Manage Plugins.”
In the “Available” tab, search for and install the “GitHub Plugin.” This plugin allows Jenkins to interact with your GitHub repository.
Set Up a GitHub Personal Access Token:

To enable Jenkins to interact with your GitHub repository, you’ll need to create a Personal Access Token with the necessary permissions. Go to GitHub and follow these steps:
Navigate to your GitHub Settings > Developer settings > Personal access tokens.
Click “Generate token” and give it a name, e.g., “Jenkins CI.”
Select the necessary permissions (usually “repo” and “admin:repo_hook” for repository access).
Generate the token and save it securely.
Create a New Jenkins Job:

In Jenkins, create a new job by clicking “New Item.”
Enter a name for your job and select the “Freestyle project” option.
Configure the Jenkins Job:

In the job configuration:
In the “Source Code Management” section, select “Git” and provide your GitHub repository URL.
Under “Credentials,” click “Add” to add your GitHub Personal Access Token as a secret credential.
In the “Build Triggers” section, select “GitHub hook trigger for GITScm polling.” This setting enables Jenkins to build when changes are pushed to the GitHub repository.
Define Build Steps:

In the “Build” section, add the build steps specific to your project. This may include commands to compile your code, run tests, and generate build artifacts.
Save and Build:

Save your Jenkins job configuration, and Jenkins will automatically trigger builds whenever changes are pushed to your GitHub repository.
GitHub Webhook Configuration:

To ensure that GitHub notifies Jenkins of changes, configure a webhook in your GitHub repository:
Go to your GitHub repository > Settings > Webhooks.
Click “Add webhook.”
Set the Payload URL to your Jenkins server’s webhook URL (usually http://jenkins-server/github-webhook/).
Set the Content type to “application/json.”
Choose the events that should trigger the webhook (e.g., “Push events”).
Add a secret if needed for additional security.
Save the webhook.
Test the CI Process:

Make a change to your GitHub repository and push it.
GitHub will trigger a webhook to Jenkins, which will start the CI build.
Monitor the Jenkins build logs to ensure that your CI process works as expected.

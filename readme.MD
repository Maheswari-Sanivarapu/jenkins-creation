Create Jenkins master, Jenkins agent EC2 instances. Update R53 records.
Add the Jenkins agent Ec2 instance private-ip in Settings-->node-->new node
Install below plugins when you started Jenkins.

Install the below Plugins:

Pipeline stage view
Pipeline Utility Steps
AWS Credentials
AWS Steps
Rebuild
Ansi Color
SonarScanner
Restart Jenkins once plugins are installed

Manage Credentials:
We need to add ssh credentials for Jenkins to connect to agent. I am using ID as ssh-auth.
We need to add aws credentials for Jenkins to connect with AWS for deployments. I am using
aws-creds
aws-creds-prod
aws-creds-dev
Connect to SonarQube EC2 instance from EC2 connect in AWS console UI.Get the password after connecting using EC2 connect then sonarqube server will be launched
We need to get security token from my account in sonarqube.
We need to add Sonar credentials for Jenkins to connect with Sonar Server. I am using sonar-auth as ID.

EKS
Make sure roboshop namespace exist.
make sure EKS control plane allows Jenkins agent to connect on port 443 HTTPS.

steps to install sonarqube in jenkins:

1. create the EC2 instance by searching the sonarqube in Marketplace AMI 
2. Launch the EC2 instance
3. In Jenkins install Sonarscanner plugin under settings--> plugins--> available plugins
4. Then in Jenkins Goto Manage Jenkins --> Tools --> SonarQube Scanner installations option will be enabled --> Add Sonarqube scanner --> after adding this plugin we will options to add the sonarqube version . Sonarqube scanner tool will be enabled
5. Now this tool i.e. sonarqube agent need to know where the sonarqube server is present so we are adding the URL of sonarqube i.e. http://<public-ip-of-sonarqube-server>:9000 under manage jenkins ---> system ---> sonarqube servers --> sonarqube installations --> Add Sonarqube (here name should be same as name used for tool in step-4)
6. Get the security from sonarqube under this http://<public-ip-of-sonarqube-server>:9000 under My Account-->Security --> Generate Tokens --> select type as Global Analysis Token
7. Add the Global Analysis Token generated created in step-6 in jenkins under manage settings--> credentials--> add the token by selecting type as secret text

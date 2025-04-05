Create a ec2 instance 
Create a security inbound rule
Update the security inbound rule with custom tcp with 8080 port 
Install the java & jenkin on ec2 machine
sudo apt update
sudo apt-get install openjdk-17-jdk
sudo apt-get install openjdk-17-jdk
sudo apt install jenkins
sudo wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
   /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys  5BA31D57EF5975CA
sudo apt-get install jenkins
   
Login to jenkins create a user for first time
install the plugins AWS credentials to jenkins
Create the user in AWS IAM with s3 policy
Save the user details.
create the aws user in credentials in jenkins using the save data 
use below in pipeline to get backup over s3

pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-s3-creds')
        AWS_SECRET_ACCESS_KEY = credentials('aws-s3-creds')
        BUCKET = 'websitebucket-niks'
    }

    stages {
        stage('Archive Artifacts') {
            steps {
                // Build and archive
                sh 'zip -r build.zip *'
                archiveArtifacts artifacts: 'build.zip'
            }
        }

        stage('Upload to S3') {
            steps {
                sh '''
                aws s3 cp build.zip s3://$BUCKET/backups/build-$(date +%F-%H-%M).zip
                '''
            }
        }
    }
}


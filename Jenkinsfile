pipeline {
    agent any
    
    stages{
        stage ('gitpull') {
            steps{
                git 'https://github.com/Gaikwad-07/pythonnew.git'
            }
            
        }        
        stage ('Build') {
            steps{
                sh '''cd /var/lib/jenkins/workspace/python-spacy-pro1
sudo apt-get install python3-pip python3-dev nginx -y
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install python3-venv -y
sudo pip3 install virtualenv'''

            }
        }
        stage ('Test') {
            steps{
                sh '''#!/bin/bash
cd /var/lib/jenkins/workspace/python-spacy-pro1
sudo virtualenv env
source env/bin/activate
sudo pip3 install -r requirements.txt
cd /var/lib/jenkins/workspace/python-spacy-pro1
systemctl start nginx
sudo pip3 install gunicorn
sudo pip3 install requests'''
            }
        }
        stage ('deploy') {
            steps{
sh 'pip3 install django'               
sh 'sudo ufw allow 8000'
sh 'gunicorn --bind 0.0.0.0:8001 demo_spacy.wsgi &'
            }
        }    
    }
}

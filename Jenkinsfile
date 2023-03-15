pipeline {
    agent any
    
    stages{
        stage ('gitpull') {
            steps{
                git 'https://github.com/Gaikwad-07/pythonnew.git'
            }
            
        }        
        stage ('Built') {
            steps{
                sh '''cd /var/lib/jenkins/workspace/python-spacy-pro
sudo apt-get install python3-pip python3-dev nginx -y
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install python3-venv -y
sudo pip3 install virtualenv
cd /var/lib/jenkins/workspace/python-spacy-pro
virtualenv env'''
            }
        }
        stage ('Test') {
            steps{
                sh '''#!/bin/bash
source env/bin/activate
sudo pip3 install -r requirements.txt
cd /var/lib/jenkins/workspace/python-spacy-pro
systemctl start ngix
sudo pip3 install gunicorn
sudo ufw enable'''
            }
        }
        stage ('deploy') {
            steps{
                sh '''#!/bin/bash
sudo ufw allow 8000
gunicorn --bind 0.0.0.0:8000 demo_spacy.wsgi &'''
            }
        }    
    }
}

pipeline {
    agent any
    
    stages{
        stage ('gitpull') {
            steps{
                git 'https://github.com/Gaikwad-07/python-spacy-pro.git'
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
pip3 install -r requirements.txt
pip3 install django==3.0.7
cd /var/lib/jenkins/workspace/python-spacy-pro
systemctl start ngix
pip3 install gunicorn
pip3 install pandas==1.5.0'''
            }
        }
        stage ('deplpoy') {
            steps{
                sh '''#!/bin/bash
sudo ufw allow 8000
pip3 install spacy 
pip3 install request
gunicorn --bind 0.0.0.0:8000 demo_spacy.wsgi &'''
            }
        }    
    }
}
pipeline {
    agent any
    
    stages{ 
        stage ('Built') {
            steps{
                sh '''cd /var/lib/jenkins/workspace/python-pipeline
sudo apt-get install python3-pip python3-dev nginx -y
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install python3-venv -y
sudo pip3 install virtualenv'''
            }
        }    

        stage ('Test') {
            steps{
                sh '''#!/bin/bash
cd /var/lib/jenkins/workspace/python-pipeline
sudo virtualenv env
source env/bin/activate
sudo pip3 install -r requirements.txt
cd /var/lib/jenkins/workspace/python-pipeline
systemctl start ngix
sudo pip3 install gunicorn
sudo pip3 install requests'''
            
            }
        }

        stage ('deploy') {
            steps{
                sh 'sudo ufw allow 8000'
                sh 'sudo gunicorn --bind 0.0.0.0:8000 demo_spacy.wsgi:application &'
                
            }
        }
    }
}            

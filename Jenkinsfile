pipeline {
    agent any

    environment {
        ANSIBLE_VAULT_PASSWORD_FILE = credentials ('ansible-vault-password-file')
        ACCESS_KEY = credentials ('ACCESS_KEY')
        SECRET_KEY = credentials ('SECRET_KEY')
        ANSIBLE_HOSTS="inventory/ec2.py"
        EC2_INI_PATH="inventory/ec2.ini"
        docker_credentials = credentials ('docker_credentials')
        DOCKERKEY = credentials ('DOCKER-PASSWORD')
    }

    stages {
        stage('CONVERT INFRASTRUCTURE FILE TO EXECUTABLE') {
            steps {
                sh 'ls'
                sh 'chmod -x script.sh'  
                sh 'chmod -x play_ansible_book.sh'
            }
        }

        stage('RUN INFRASTRUCTURE BASH SCRIPT') {
            steps {
                sh 'sh create_infrastructure.sh'
           }
        } 

        stage('PLAY ANSIBLE BOOK') {
            steps {
                sh 'sh play_ansible_book.sh'
                sh 'ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook ansible-job/playbook/playbookbroker.yml -i ansible-job/inventory/hosts/ec2.py -vvvvv'            
                }
        }  
    }
}
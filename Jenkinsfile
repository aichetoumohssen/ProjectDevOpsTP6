pipeline {
    agent any

    environment {
        ANSIBLE_INVENTORY = 'ansible/hosts.ini'
        ANSIBLE_PLAYBOOK = 'ansible/deploiement.yml'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/aichetoumohssen/ProjectDevOpsTP6.git'
            }
        }

        stage('Install Tools') {
            steps {
                sh 'sudo apt-get update'
                sh 'sudo apt-get install -y ansible openjdk-17-jdk maven'
            }
        }

        stage('Build Spring Boot App') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy with Ansible') {
            steps {
                ansiblePlaybook(
                    playbook: "${ANSIBLE_PLAYBOOK}",
                    inventory: "${ANSIBLE_INVENTORY}"
                )
            }
        }
    }
}



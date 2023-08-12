pipeline {
    agent any

    environment {
        ANSIBLE_HOST = 'your-ansible-host'
        ANSIBLE_PLAYBOOK_PATH = 'path/to/ansible/playbook'
    }

    stages {
        stage('Checkout') {
            steps {
                dir("${WORKSPACE}") {
                    git branch: "main", url: 'https://github.com/wasim094/ansible.git'
                }
            }
        }
        stage('Build') {
            steps {
                withMaven(maven: 'Maven 3.8.6') {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Deploy and Restart') {
            steps {
                // Copy WAR file to remote host
                sh "ansible-playbook -i $ANSIBLE_HOST, -u remote-user $ANSIBLE_PLAYBOOK_PATH/deploy_restart.yml"
            }
        }
    }
}

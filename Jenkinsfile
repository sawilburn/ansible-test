pipeline {
    agent any
    
    environment {
        ANSIBLE_PATH = tool name: 'Ansible', type: 'org.jenkinsci.plugins.ansible.AnsibleInstallation'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Add the ansible binary to PATH
                    env.PATH = "${env.ANSIBLE_PATH}:${env.PATH}"
                    
                    // Run the playbook
                    sh """
                        ansible --version
                        ansible-playbook -i inventory/hosts.yml playbooks/test-playbook.yml
                    """
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}


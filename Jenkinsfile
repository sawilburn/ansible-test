pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository containing the playbook and inventory
                checkout scm
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Run the Ansible playbook inside the Ansible container
                    docker.image('1c77c4a65f6fcfd63b25954f9f3146f8f5e586e830a7d985908d005013e5eef2').inside('-v $WORKSPACE:/workspace') {
                        sh """
                        cd /workspace
                        ansible --version
                        ansible-playbook -i inventory/hosts.yml playbooks/test-playbook.yml
                        """
                    }
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


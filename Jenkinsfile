pipeline {
    agent any

    environment {
        ANSIBLE_CONFIG = "${WORKSPACE}/ansible.cfg"
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/badrijv/musicfile.git', branch: 'main'
            }
        }

        stage('Verify Ansible Installed') {
            steps {
                sh '''
                    echo ">>> Jenkins user:"
                    whoami
                    id

                    echo ">>> Checking Ansible:"
                    which ansible || true
                    ansible --version || { echo "Ansible NOT installed!"; exit 1; }
                '''
            }
        }

        stage('Ping Localhost') {
            steps {
                sh '''
                    ansible all -i inventory.ini -m ping
                '''
            }
        }

        stage('Run Playbook on EC2') {
            steps {
                sh '''
                    ansible-playbook -i inventory.ini playbook.yml
                '''
            }
        }
    }
}

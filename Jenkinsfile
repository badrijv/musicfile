
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/badrijv/musicfile.git', branch: 'main'
            }
        }

        stage('Ping EC2') {
            steps {
                    sh """
                        ansible all -i inventory.ini -m ping
                    """
            }
        }

        stage('Run Playbook') {
            steps {
                    sh """
                        ansible-playbook -i inventory.ini playbook.yml
                    """
            }
        }
    }
}

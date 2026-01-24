
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

        stage('Ping EC2') {
            steps {
                    sh """
                        ansible all -i inventory.ini -m ping
                        
echo ">>> Effective Jenkins user:"
      whoami
      id
      echo ">>> Testing passwordless sudo:"
      sudo -n true && echo "OK (sudo works without password)" || echo "FAIL (sudo requires password)"

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

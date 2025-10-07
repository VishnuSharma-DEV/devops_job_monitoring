pipeline {
    agent any
    stages {
        stage('Run Ansible Playbook') {
            steps {
                sh 'docker exec ansible ansible-playbook -i /ansible/inventory /ansible/playbook.yml'
            }
        }
    }
}
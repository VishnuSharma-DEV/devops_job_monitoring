pipeline {
    agent any
    triggers {
        cron('H/5 * * * *') // Runs every 5 minutes
    }
    stages {
        stage('Run Ansible Playbook') {
            steps {
                sh 'docker exec ansible ansible-playbook -i /ansible/inventory /ansible/playbook.yml'
            }
        }
    }
}

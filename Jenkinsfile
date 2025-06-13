pipeline {
    agent any

    environment {
        APP_NAME = "springapp"
        REMOTE_HOST = "ec2-user@172.31.18.134"
    }

    stages {
        stage ('clone') {
            steps {
                git 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }

        stage ('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage ('Archive artifacts'){
            steps {
                archiveArtifacts artifacts : 'target/*jar' , fingerprint: true
            }
        }

        stage ('Deploy with ansibele') {
            steps{
                ansiblePlaybook credentialsId: 'ansible-ssh', playbook: 'deploy.yml'
            }

        }
    }
}
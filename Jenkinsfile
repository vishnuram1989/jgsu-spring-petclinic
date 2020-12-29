pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Clone Project') {
            steps {
                git branch: 'master', credentialsId: 'gitcredentials', url: 'https://github.com/vishnuram1989/jgsu-spring-petclinic.git'
            
            }
            
        }
        
        stage('Clean') {
            steps {
                sh 'cd jgsu-spring-petclinic && ./mvnw clean'
            }
        }
        
        stage('Compile ') {
            steps {
                sh 'cd jgsu-spring-petclinic && ./mvnw compile '
            }
        }
        
        stage('Package ') {
            steps {
                sh 'cd jgsu-spring-petclinic && ./mvnw package'
            }
        }
    }
}

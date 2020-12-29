pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Clone Project') {
            steps {
                git branch: 'main', credentialsId: 'gitcredentials', url: 'https://github.com/vishnuram1989/jgsu-spring-petclinic.git'
            
            }
            
        }
        
        stage('Clean') {
            steps {
                sh './mvnw clean'
            }
        }
        
        stage('Compile ') {
            steps {
                sh './mvnw compile '
            }
        }
        
        stage('Package ') {
            steps {
                sh './mvnw package'
            }

            post {
            success {
                junit '**/target/surefire-reports/*.xml'
                archiveArtifacts  '**/target/*.jar'
            }
        }
    }
}

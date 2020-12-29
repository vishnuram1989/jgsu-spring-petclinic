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

        stage('Deploy for production') {
            when {
                branch 'main'  
            }
            steps {
                input message: 'Proceed to deploy this site on Production? (Click "Proceed" to continue)'

                sh 'echo "Deploying to production" '
                //sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'echo "Deploying to production completed" '
            }
        }
    }
}

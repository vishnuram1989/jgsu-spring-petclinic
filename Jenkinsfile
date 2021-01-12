pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Clone Project') {
            steps {
                git branch: 'main', credentialsId: 'gitcredentials', url: 'https://github.com/vishnuram1989/jgsu-spring-petclinic.git'
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh "exit 1"
        }
            
            }
            
        }
        
        stage('Clean') {
            steps {
                sh './mvnw clean'
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh "exit 1"
        }
            }
        }
        
        stage('Compile ') {
            steps {
                sh './mvnw compile '
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh "exit 1"
        }
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

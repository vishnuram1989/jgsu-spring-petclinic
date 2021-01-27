pipeline {
    agent any

    triggers {
        //pollSCM('* * * * *')
        githubPush()
        
    }

    stages {      
        stage('Clean') {
            steps {
                sh './mvnw clean'
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh "exit 1"
        }
            }
        }
    }

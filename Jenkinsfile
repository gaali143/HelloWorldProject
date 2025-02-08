pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/gaali143/HelloWorldProject.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'  // Use Gradle if needed: sh 'gradle build'
            }
        }

        stage('Deploy to Azure') {
            steps {
                withAzureCLI(credentialsId: 'azure-credentials') {
                    sh '''
                    az webapp deployment source config-zip --resource-group MyJenkins \
                    --name HelloTeam --src target/*.jar
                    '''
                }
            }
        }
    }
}

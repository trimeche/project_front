pipeline {
    agent  any 
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('SonarQube analysis') {
            steps {
            script{
            def scannerHome = tool 'SonarQube Scanner 2.8';
            withSonarQubeEnv('SonarQube') {
                sh "${tool("SonarQube Scanner 2.8")}/bin/sonar-scanner \
                    -Dsonar.projectKey=sonarqubetest \
                    -Dsonar.projectName=sonarqubetest"
            }
            }
        }
    }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}



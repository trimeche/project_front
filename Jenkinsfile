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
            def scannerHome = tool 'sonarqube';
            withSonarQubeEnv('SonarQube') {
                sh "${tool("sonarqube")}/bin/sonar-scanner \
                    -Dsonar.projectKey=sonarqubetest \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://127.0.0.1:9000 \
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



pipeline {
    agent any
    tools {
        // Ensure that you reference the correct SonarQube Scanner name configured in Jenkins
        sonarQubeScanner 'SonarQube_Scanner'
    }
    environment {
        SONARQUBE = 'SonarQube'  // Your SonarQube server name configured in Jenkins
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/naveenkumar2412/jenkins-sonar.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                        sh '''
                            sonar-scanner \
                            -Dsonar.projectKey=sonar-example \
                            -Dsonar.host.url=http://your-sonarqube-server-url \
                            -Dsonar.login=your-sonarqube-token
                        '''
                    }
                }
            }
        }
        stage('Dependency-Check Analysis') {
            steps {
                echo 'Running Dependency-Check analysis...'
            }
        }
    }
    post {
        always {
            echo 'Build finished.'
        }
    }
}



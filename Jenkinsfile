pipeline {
    agent any
    tools {
        // Correct tool type for SonarQube Scanner
        SonarRunner 'SonarQube_Scanner'  // Ensure the name matches your SonarQube configuration
        jdk 'JDK11'  // JDK version you have installed
        maven 'Maven3'  // Ensure Maven is configured correctly
    }
    environment {
        SONARQUBE = 'SonarQube'  // Match the SonarQube server configuration name
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



pipeline {
    agent any
    tools {
        // Use the correct SonarQube tool type
        sonarRunner 'SonarQube_Scanner'  // The name should match your SonarQube installation name in Jenkins
        jdk 'JDK8'  // JDK version you have installed
        maven 'Maven3'  // Maven installation (if applicable)
    }
    environment {
        SONARQUBE = 'SonarQube'  // This should match your SonarQube server configuration
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


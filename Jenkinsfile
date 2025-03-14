pipeline {
    agent any
    tools {
        // Specify Maven tool if not already configured
        maven 'Maven3'
    }
    environment {
        SONARQUBE = 'SonarQube'  // Define the SonarQube installation in Jenkins
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
                        // Run the SonarQube scanner with required parameters
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


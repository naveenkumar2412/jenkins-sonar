pipeline {
    agent any
    tools {
        jdk 'JDK11'  // JDK version you have installed
        maven 'Maven3'  // Maven configuration
    }
    environment {
        SONARQUBE = 'SonarQube'  // SonarQube server name as configured in Jenkins
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
                            -Dsonar.projectKey=jenkins \
                            -Dsonar.host.url=http://65.2.129.154:9000 \
                            -Dsonar.login=jenkins
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



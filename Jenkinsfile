pipeline {
    agent any
    tools {
        jdk 'JDK11'
        maven 'Maven3'
    }
    environment {
        SONARQUBE = 'SonarQube'  // SonarQube server name as configured in Jenkins
        SONAR_TOKEN = 'sqa_00223b59a3758b1269eb00c61abfbd454f4cd53b'  // Replace with the token you generated
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
                            docker run --rm \
                            -v $(pwd):/usr/src \
                            sonarsource/sonar-scanner-cli:latest \
                            sonar-scanner \
                            -Dsonar.projectKey=jenkins \
                            -Dsonar.host.url=http://13.234.117.178:9000 \
                            -Dsonar.login=$SONAR_TOKEN
                        '''
                    }
                }
            }
        }
        stage('Dependency-Check Analysis') {
            steps {
                script {
                    // Run Dependency-Check analysis with Maven plugin
                    echo 'Running Dependency-Check analysis...'
                    sh 'mvn org.owasp:dependency-check-maven:check'
                }
            }
        }
    }
    post {
        always {
            echo 'Build finished.'
        }
    }
}




pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token') // Jenkins credential with your token
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/fayelise/sonar-test.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    script {
                        // Use the manually installed scanner directly
                        sh """
                        /opt/sonar-scanner/bin/sonar-scanner \
                            -Dsonar.projectKey=sonar-test \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.login=$SONAR_TOKEN
                        """
                    }
                }
            }
        }
    }
}

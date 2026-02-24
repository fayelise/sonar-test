pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token')
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
                def scannerHome = tool 'sonar-scanner'

                sh """
                ${scannerHome}/bin/sonar-scanner \
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

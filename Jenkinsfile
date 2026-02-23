pipeline {
    agent any

    tools {
        // Must exist in Manage Jenkins → Global Tool Configuration
        jdk 'jdk17'
    }

    stages {

        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

       stage('Sonar-Report') {
    steps {
        withCredentials([string(credentialsId: 'jenkins-token', variable: 'SONAR_TOKEN')]) {
            bat "mvn clean install org.sonarsource.scanner.maven:sonar-maven-plugin:4.0.0.4121:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.token=%SONAR_TOKEN%"
        }
    }
}
    }
}

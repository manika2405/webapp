pipeline {
    agent any

    tools {
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
    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }
    steps {
        bat '''
        mvn clean install org.sonarsource.scanner.maven:sonar-maven-plugin:4.0.0.4121:sonar ^
        -Dsonar.host.url=http://localhost:9000 ^
        -Dsonar.token=%SONAR_TOKEN%
        '''
    }
}
    }
}

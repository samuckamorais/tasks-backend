pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests') {
             steps {
                bat 'mvn test'
             }
        }
        stage ('Sonar Analysis') {
             environment {
                scannerHome = tool 'SONAR_SCANNE'
             }
             steps {
                withSonarQubeEnv('SONAR_LOCAL'){
                    bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=82c3fb81c21e3f8f08421ee9ed31c89c885e70bc -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"
                }
             }
        }
    }
}


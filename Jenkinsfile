pipeline {
    agent any
    
    environment {
        TOMCAT_USER = "admin"
        TOMCAT_PASS = "admin123"
        TOMCAT_URL = "http://localhost:8080/manager/text"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://github.com/vaadin/addressbook.git'
            }
        }
        
        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
                bat "curl --upload-file target/addressbook.war \"%TOMCAT_USER%:%TOMCAT_PASS%@%TOMCAT_URL%/deploy?path=/addressbook&update=true\""
            }
        }
    }
}

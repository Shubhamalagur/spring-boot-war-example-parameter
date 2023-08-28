pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('SCM checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Shubhamalagur/spring-boot-war-example.git']])
            }
        }
        stage('Sonar stage') {
            steps {
                echo "running sonar scan"
                    }
        }
        stage('build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('deploy') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://13.233.133.196:8081')], contextPath: '/pipe', war: '**/*.war'
            }
        }    
    }
}



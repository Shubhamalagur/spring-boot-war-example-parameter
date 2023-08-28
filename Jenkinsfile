pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('SCM checkout') {
            agent {
              label {
                    label "Captain_Philip"
                     }
                    }
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Shubhamalagur/spring-boot-war-example.git']])
                             }
         }
        stage('Sonar stage') {
            agent {
              label {
                    label "Captain_Roger"
                     }
                    }
            steps {
                echo "running sonar scan"
                    }
        }
        stage('build') {
            agent {
              label {
                    label "Captain_Philip"
                     }
                    }
            steps {
                sh 'mvn clean install'
            }
        }
        stage('deploy') {
            agent {
              label {
                    label "Captain_Roger"
                     }
                    }
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://13.233.133.196:8081')], contextPath: '/logo', war: '**/*.war'
            }
        }    
    }
}



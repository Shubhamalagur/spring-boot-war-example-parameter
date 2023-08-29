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
          stage('Sonarstage'){
                parallel{
                    stage('SonarstageA') {
                        agent {
                          label {
                                label "Captain_Roger"
                                 }
                                }
                        steps{
                        echo "This is branch a"
                        }
                    }
                    stage('SonarstageB') {
                        agent {
                          label {
                                label "Captain_Philip"
                                 }
                                }
                        steps{
                        echo "This is branch b"
                        }
                    }
                }}
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
                    label "Captain_Philip"
                     }
                    }
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://13.232.88.151:8081')], contextPath: '/logo', war: '**/*.war'
            }
        }
	stage('Email'){
		agent {
		label {
			label "Captain_Philip"
			} 
			}
		steps {
			emailext body: '''${env.PROJECT_NAME} - Build # ${env.BUILD_NUMBER} - ${env.BUILD_STATUS}:Check console output at ${env.BUILD_URL} to view the results.''', subject: '${env.PROJECT_NAME} - Build # ${env.BUILD_NUMBER} - ${env.BUILD_STATUS}!', to: 'shubhamalagur@gmail.com'}   
    }
}
}



pipeline {
    agent any
	
	tools {
        maven 'Maven'
    }
    
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'master', description: 'Enter the Git branch name')
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    echo "Checking out ${params.BRANCH_NAME} branch..."
                    checkout([$class: 'GitSCM', 
                              branches: [[name: "*/${params.BRANCH_NAME}"]],
                              userRemoteConfigs: [[url: 'https://github.com/Shubhamalagur/spring-boot-war-example-parameter.git']]])
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    echo "Building ${params.BRANCH_NAME} branch..."
                    sh 'mvn clean install'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    def targetTomcat = ''
                    
                    if (params.BRANCH_NAME == 'master') {
                        targetTomcat = 'tomcat-1'
                    } else if (params.BRANCH_NAME == 'Dev') {
                        targetTomcat = 'tomcat-2'
                    } else if (params.BRANCH_NAME == 'Test') {
                        targetTomcat = 'tomcat-3'
                    }
                    
                    if (targetTomcat == 'tomcat-1') 
						{
							echo "Deploying ${params.BRANCH_NAME} branch to ${targetTomcat}..."
							 deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://43.204.114.96:8081')], contextPath: '/master', war: '**/*.war'
						} 
					else if
						{
							echo "Deploying ${params.BRANCH_NAME} branch to ${targetTomcat}..."	
							deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://43.204.114.96:8081')], contextPath: '/Dev', war: '**/*.war'
						}
					else if
						{
							echo "Deploying ${params.BRANCH_NAME} branch to ${targetTomcat}..."	
							deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://43.204.114.96:8081')], contextPath: '/Test', war: '**/*.war'
						}	
					else {
                        echo "Branch ${params.BRANCH_NAME} is not configured for deployment."
                    }
                }
            }
        }
    }
}

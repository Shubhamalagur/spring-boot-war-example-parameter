pipeline {
    agent any
    
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'feature', description: 'Enter the Git branch name')
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    echo "Checking out ${params.BRANCH_NAME} branch..."
                    checkout([$class: 'GitSCM', 
                              branches: [[name: "*/${params.BRANCH_NAME}"]],
                              userRemoteConfigs: [[url: 'YOUR_GITHUB_REPO_URL']]])
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    echo "Building ${params.BRANCH_NAME} branch..."
                    // Add build actions specific to the branch
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    def targetTomcat = ''
                    
                    if (params.BRANCH_NAME == 'feature') {
                        targetTomcat = 'tomcat-1'
                    } else if (params.BRANCH_NAME == 'develop') {
                        targetTomcat = 'tomcat-2'
                    } else if (params.BRANCH_NAME == 'master') {
                        targetTomcat = 'prod'
                    }
                    
                    if (targetTomcat) {
                        echo "Deploying ${params.BRANCH_NAME} branch to ${targetTomcat}..."
                        // Add deployment actions specific to the targetTomcat
                    } else {
                        echo "Branch ${params.BRANCH_NAME} is not configured for deployment."
                    }
                }
            }
        }
    }
}

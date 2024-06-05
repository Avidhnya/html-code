pipeline {
    agent any

    environment {
        SSH_KEY = credentials('my-ssh') // ID of the SSH key added in Jenkins credentials
        GIT_REPO_URL = 'https://github.com/Avidhnya/html-code.git'
        GIT_BRANCH = 'main'
        NGINX_SERVER = '16.170.251.75'
        DEPLOY_DIR = '/usr/share/nginx/html'
        USER = 'ec2-user' // Change this to your actual username on the Nginx server
	GIT_CREDENTIALS_ID = 'git access' // ID of the GitHub credentials added in Jenkins
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: '''${main}''', url: '''${https://github.com/Avidhnya/html-code.git}''', credentialsId: '''${git access}'''
            }
        }
        
        stage('Build') {
            steps {
                // Add your build steps here
                echo 'Building the application...'
            }
        }
        
        stage('Test') {
            steps {
                // Add your test steps here
                echo 'Running tests...'
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    // Deploy to Nginx server using SSH
                    sh '''
                    ssh -o StrictHostKeyChecking=no -i ${my-ssh} ${ec-user}@${16.170.251.75} << 'ENDSSH'
                        cd ${/usr/share/nginx/html}
                        git pull origin ${main}
                        ./deploy.sh
                    ENDSSH
                    '''
                }
            }
        }
    }

post {
        always {
            cleanWs() // Clean workspace after build
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs for errors.'
        }
    }	
}



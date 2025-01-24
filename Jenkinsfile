pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Get code from GitHub repository
                git branch: 'master', 
                    url: 'https://github.com/NikhilCyberk/basic-react-app.git'
            }
        }
        
        stage('Install') {
            steps {
                // Install Node dependencies
                bat 'npm install'
            }
        }
        
        stage('Lint') {
            steps {
                script {
                    try {
                        bat 'npm run lint'
                    } catch (err) {
                        // Don't fail the build, but mark it as unstable
                        unstable(message: "Linting issues found")
                        // Continue with the build
                        echo "Lint issues found, but continuing with build..."
                    }
                }
            }
        }
        
        stage('Build') {
            steps {
                // Create production build
                bat 'npm run build'
            }
        }
        
        stage('Deploy') {
            steps {
                echo "deploy success"
            }
        }
    }
    
    post {
        success {
            echo 'Build and deployment successful!'
        }
        unstable {
            echo 'Build completed with some issues.'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}

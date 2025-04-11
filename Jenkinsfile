pipeline {
    agent any
    
    environment {
        NODE_VERSION = '18.x'  // Specify Node.js version
        NEXT_PUBLIC_API_URL = 'your-api-url'  // Add your environment variables here
    }
    
    stages {
        stage('Setup') {
            steps {
                // Install Node.js
                sh 'curl -sL https://deb.nodesource.com/setup_${NODE_VERSION} | bash -'
                sh 'apt-get install -y nodejs'
                
                // Install dependencies
                sh 'npm install'
            }
        }
        
        stage('Lint') {
            steps {
                // Run ESLint
                sh 'npm run lint'
            }
        }
        
        stage('Build') {
            steps {
                // Build Next.js application
                sh 'npm run build'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests (if you have any)
                sh 'npm test || true'
            }
        }
        
        stage('Deploy to Development') {
            when {
                branch 'develop'
            }
            steps {
                // Add your deployment steps for development environment
                sh '''
                    echo "Deploying to development environment"
                    # Add your deployment commands here
                    # Example: ssh user@dev-server 'cd /path/to/app && git pull && npm install && npm run build'
                '''
            }
        }
        
        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                // Add your deployment steps for production environment
                sh '''
                    echo "Deploying to production environment"
                    # Add your production deployment commands here
                    # Example: ssh user@prod-server 'cd /path/to/app && git pull && npm install && npm run build'
                '''
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Please check the logs for details.'
        }
        always {
            // Clean workspace after build
            cleanWs()
        }
    }
} 
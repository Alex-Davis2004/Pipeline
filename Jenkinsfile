pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the Python application...'
                sh 'python3 setup.py install'  // Using setup.py for building the application
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'pytest'  // Using pytest as the test framework
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code...'
                sh 'pylint app.py test_app.py'  // Using Pylint for code analysis
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'safety check'  // Using Safety for security scanning
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                sh 'ssh user@staging-server "cd /path/to/app && git pull origin main && docker-compose up -d"'  // Deploying using Docker Compose on a staging server
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'pytest --config=staging_config.ini'  // Running integration tests with a specific config
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                sh 'ssh user@production-server "cd /path/to/app && git pull origin main && docker-compose up -d"'  // Deploying using Docker Compose on a production server
            }
        }
    }

    post {
        success {
            mail to: 'your_email@example.com',
                 subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Good news! The build was successful. Check it out at ${env.BUILD_URL}."
        }
        failure {
            mail to: 'your_email@example.com',
                 subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Oops! The build failed. Check the logs at ${env.BUILD_URL}."
        }
    }
}

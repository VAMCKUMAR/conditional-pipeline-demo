pipeline {
    agent any

    parameters {
        string(name: 'DEPLOY_ENV', defaultValue: 'dev', description: 'Deployment environment')
    }

    environment {
        BUILD_OWNER = 'Vamshi'
    }

    stages {

        stage('Checkout') {
            steps {
                echo "🔁 Checking out code..."
                checkout scm
            }
        }

        stage('Build') {
            when {
                branch 'main'
            }
            steps {
                echo "🏗️ Building the project (only on main branch)"
            }
        }

        stage('Test') {
            when {
                anyOf {
                    branch 'main'
                    branch 'dev'
                }
            }
            steps {
                echo "🧪 Running tests (on main or dev)"
            }
        }

        stage('Deploy') {
            when {
                expression { return params.DEPLOY_ENV == 'prod' }
            }
            steps {
                echo "🚀 Deploying to production!"
            }
        }

        stage('Notify') {
            when {
                environment name: 'BUILD_OWNER', value: 'Vamshi'
            }
            steps {
                echo "📣 Sending notification to ${env.BUILD_OWNER}"
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}

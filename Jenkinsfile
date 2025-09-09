@Library('jenkins-shared-libs') _

pipeline {
    agent any
    
    environment {
        APP_VERSION = generateVersion()
    }
    
    stages {
        stage('Checkout') {
            steps {
                sendNotification("Starting build for API", "INFO")
                echo "Code checked out successfully"
                echo "Build version: ${APP_VERSION}"
            }
        }
        
        stage('Build & Test') {
            agent { label 'build-heavy' }
            steps {
                sendNotification("Building and testing API...", "INFO")
                
                // Simulation d'un build Node.js
                sh '''
                    echo "📦 Installing dependencies..."
                    # npm install
                    echo "🔨 Building application..."
                    # npm run build
                    echo "🧪 Running tests..."
                    # npm test
                '''
                
                sendNotification("Build and tests completed successfully", "SUCCESS")
            }
        }
        
        stage('Quality Gate') {
            steps {
                sendNotification("Running quality analysis...", "INFO")
                
                // Simulation SonarQube
                sh 'echo "🔍 Running SonarQube analysis..."'
                // sonarqube analysis would go here
                
                sendNotification("Quality gate passed", "SUCCESS")
            }
        }
        
        stage('Security Scan') {
            agent { label 'build-heavy' }
            steps {
                sendNotification("Running security scans...", "INFO")
                
                // Simulation security scan
                sh '''
                    echo "🔒 Running dependency check..."
                    # npm audit
                    echo "🐳 Scanning Docker image..."
                    # trivy scan would go here
                '''
                
                sendNotification("Security scan completed", "SUCCESS")
            }
        }
        
        stage('Package') {
            steps {
                sendNotification("Creating artifacts...", "INFO")
                
                sh '''
                    echo "📦 Creating package..."
                    mkdir -p dist
                    echo "API Build ${APP_VERSION}" > dist/api-${APP_VERSION}.txt
                '''
                
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
                sendNotification("Artifacts created and archived", "SUCCESS")
            }
        }
    }
    
    post {
        success {
            sendNotification("🎉 Pipeline completed successfully! Version: ${APP_VERSION}", "SUCCESS")
        }
        failure {
            sendNotification("💥 Pipeline failed! Check the logs.", "FAILURE")
        }
        always {
            echo "Cleaning up workspace..."
        }
    }
}

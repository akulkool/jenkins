pipeline {
    agent any
    triggers {
        // Question 8: Nightly build at 2 AM
        cron('0 2 * * *')
        // Question 7: Poll SCM every 3 minutes
        pollSCM('H/3 * * * *')
    }
    stages {
        stage('Build') {
            steps {
                sh '/opt/homebrew/bin/mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh '/opt/homebrew/bin/mvn test'
            }
        }
        stage('Package') {
            steps {
                sh '/opt/homebrew/bin/mvn clean package'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
        success {
            echo "✅ Build successful! JAR file generated."
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}

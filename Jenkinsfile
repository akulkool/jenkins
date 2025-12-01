pipeline {
    agent any
    triggers {
        cron('* * * * *')
        pollSCM('* * * * *')
    }
    stages {
        stage('Build') {
            steps {
                sh '/opt/homebrew/bin/mvn clean compile'
            }
        }
        stage('Package') {
            steps {
                sh '/opt/homebrew/bin/mvn clean package -DskipTests'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
    post {
        success {
            echo "✅ BUILD SUCCESSFUL! JAR file generated and archived."
        }
    }
}

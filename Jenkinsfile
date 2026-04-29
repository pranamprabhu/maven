pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo "Checking out code"
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building Maven project"
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying JAR"
                sh '''
                mkdir -p /home/yit/deploy/myapp
                cp target/*.jar /home/yit/deploy/myapp/
                '''
            }
        }

        stage('Run') {
            steps {
                echo "Running application"
                sh '''
                pkill -f "java -jar" || true
                nohup java -jar /home/yit/deploy/myapp/*.jar > /home/yit/deploy/myapp/app.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline SUCCESS"
        }
        failure {
            echo "❌ Pipeline FAILED"
        }
    }
}

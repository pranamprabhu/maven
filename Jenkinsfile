pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/pranamprabhu/maven.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                mkdir -p /home/yit/deploy/myapp
                cp target/*.jar /home/yit/deploy/myapp/
                '''
            }
        }

        stage('Run') {
            steps {
                sh '''
                pkill -f "java -jar" || true
                nohup java -jar /home/yit/deploy/myapp/*.jar > app.log 2>&1 &
                '''
            }
        }
    }
}

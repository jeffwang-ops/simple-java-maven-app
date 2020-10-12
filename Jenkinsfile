pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('包制作') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('包测试') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('包发布') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}

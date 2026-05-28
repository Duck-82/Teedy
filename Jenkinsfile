pipeline {
    agent any
    tools {
        maven 'M3'   // 和上面配置的名字必须一模一样
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }
    }
}

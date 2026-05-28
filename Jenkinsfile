pipeline {
    agent any
    tools {
        // 改成你 Jenkins 全局工具配置里的 Maven 名称
        maven 'Maven' 
    }
    stages {
        stage('Maven 构建') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                }
            }
        }
        stage('PMD 代码检查') {
            steps {
                bat 'mvn pmd:pmd'
            }
        }
        stage('运行单元测试') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        stage('生成 HTML 测试报告') {
            steps {
                bat 'mvn surefire-report:report'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/site/**/*', fingerprint: true
                }
            }
        }
        stage('生成 JavaDoc 文档') {
            steps {
                bat 'mvn javadoc:javadoc'
            }
        }
    }
    post {
        always {
            echo "构建结束，产物已保存"
        }
    }
}
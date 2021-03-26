pipeline {
    agent any

    stages {
        stage('pull code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/${branch}']], extensions: [], userRemoteConfigs: [[credentialsId: 'root', url: 'git@github.com:cpleecn/hello-world.git']]])
            }
        }
        stage('publish code') {
            steps {
                cp /var/lib/jenkins/workspace/pipeline_project/* /usr/share/nginx/html
            }
        }
    }

    post {
        always {
            emailext(
                subject: '构建通知： ${PROJECT_NAME} - Build # ${BUILD_NUMBER} - ${BUILD_STATUS}',
                body: '${FILE,path="email.html"}',
                to: 'cpleecn@aliyun.com'
            )
        }
    }
}


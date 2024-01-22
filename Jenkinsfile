pipeline {
    agent { label 'dev' }
    tools {
        maven 'Maven' 
    }

    stages {
        stage('Code Clone') {
            steps {
                git url: 'https://github.com/taankdhirendra/spring-boot-war-example.git', branch: 'master'
                slackSend channel: 'project', message: 'Code Clone Done'
            }
        }
        stage('Test and Build') {
            steps {
                sh 'mvn test && mvn package'
                slackSend channel: 'project', message: 'Test and build Done'
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'test', path: '', url: 'http://54.221.91.244:8080')], contextPath: '/app', war: '**/*.war'
                slackSend channel: 'project', message: 'Deploy on test server'
            }
        }
    }
}

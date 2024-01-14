pipeline{
    agent any
    tools {
        maven 'Maven' 
    }
    stages{
        stage("Test"){
            steps{
                sh 'mvn test'
                slackSend channel: 'project', message: 'Test Job Completed'
            }
        }
        stage("Build"){
            steps{
                sh 'mvn package'
                slackSend channel: 'project', message: 'Build Job Completed'
            }
        }
        stage("Deploy on test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-1', path: '', url: 'http://54.159.198.144:8080')], contextPath: '/app', war: '**/*.war'
                slackSend channel: 'project', message: 'aap deploy on test server'
            }
        }
        stage("Deploy on prod"){
            steps{
                echo "========executing A========"
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}

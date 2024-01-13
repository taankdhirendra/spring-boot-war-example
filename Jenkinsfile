pipeline{
    agent any
    tools {
        maven 'Maven' 
    }
    stages{
        stage("Test"){
            steps{
                slackSend channel: 'project', message: 'Test Job Started'
                sh 'mvn test'
                
            }
        }
        stage("Build"){
            steps{
                slackSend channel: 'project', message: 'Build Job Started'
                sh 'mvn package'
                
            }
        }
        stage("Deploy on test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-server-one', path: '', url: 'http://54.164.80.226:8080')], contextPath: '/app', war: '**/*.war'
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

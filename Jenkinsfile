pipeline{
    agent any
    tools {
        maven 'Maven' 
    }
    stages{
        stage("Test"){
            steps{
                sh 'mvn test'
                slackSend channel: 'project', message: 'Test Completed'
            }
        }
        stage("Build"){
            steps{
                sh 'mvn package'
                slackSend channel: 'project', message: 'Build Completed'
            }
        }
        stage("Deploy on test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://44.205.245.223:8084')], contextPath: '/app', war: '**/*.war'
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

pipeline{
    agent any
    tools {
        maven 'Maven' 
    }
    stages{
        stage("Git"){
            steps{
                sh 'mvn --version'
            }
        }
        stage("Test"){
            steps{
                sh 'mvn test'
            }
        }
        stage("Build"){
            steps{
                sh 'mvn package'
            }
        }
        stage("Deploy on test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-server-one', path: '', url: 'http://54.164.80.226:8080/')], contextPath: '/app', war: '**/*.war'
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

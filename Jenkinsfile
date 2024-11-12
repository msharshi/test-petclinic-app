pipeline {
    agent any
    
    tools {
        maven 'maven'
    }
    
    stages {
        stage("Git Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/Nandini-1428/test-petclinic-app.git'
            }
        }
        stage("Compile") {
            steps {
                sh "mvn compile"
            }
        }
        stage("Test") {
            steps {
                sh "mvn test -DskipTests=true"
            }
        }
        stage("Build") {
            steps {
                sh "mvn package -DskipTests=true"
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(url: 'http://54.165.63.65:8000',
                            credentialsId: 'tomcat-server')],
                        war: 'target/*.war',
                        contextPath: 'petclinic'
            }
        }
    }
}

pipeline {
    agent any   
    stages {
        stage ('Compile Stage') {   
            steps {
                mail to:"joseph.stalin.peter@gmail.com", subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"                   
                withMaven(maven : 'Maven1') {
                    sh 'mvn clean compile'
                }
            }
        }
        stage ('Testing Stage') {
            steps {
                withMaven(maven : 'Maven1') {
                    sh 'mvn test'
                }
            }
        }
        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'Maven1') {
                    sh 'mvn deploy'
                }
            }
        }
        stage('Report') {
            steps {
               junit(testResults: 'target/surefire-reports/**/*.xml')
               archiveArtifacts 'target/*.jar,target/*.hpi'
            }
        }
    }       
        post {
        success {
            mail to:"joseph.stalin.peter@gmail.com", subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        }
        failure {
            mail to:"joseph.stalin.peter@gmail.com", subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        }
        unstable {
            mail to:"joseph.stalin.peter@gmail.com", subject:"UNSTABLE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "UNSTABLE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        }     
        changed {
            mail to:"joseph.stalin.peter@gmail.com", subject:"CHANGED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", body: "CHANGED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        }
    }
}

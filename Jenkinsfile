pipeline {
    agent any
    stages {
        stage("checkout") {
            steps {
                sh "ls"
                git branch: 'main', url: "https://github.com/bouw002/course3-jenkins-gs-spring-petclinic" 
                sh "ls"
            }
        }
        
        stage("build"){
            steps {
                sh "./mvnw package"
            }
        }
        
        stage("Capture"){
            steps {
                archiveArtifacts '**/target/*.jar'
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
                jacoco()
            }
        }
    }
    post {
        always {
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}", 
            subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]", 
            to: 'eric.bouw@local.com'
        }
    }

}
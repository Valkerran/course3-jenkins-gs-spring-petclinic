pipeline {
    agent any

    stages {        
        stage("build") {
            steps {
                sh "./mvnw package"
            }
        }
        
        stage("capture") {
                steps {
                archiveArtifacts '**/target/*.jar'
                jacoco()
                junit testResults: '**/target/surefire-reports/TEST*.xml'
            }
        }
    }
    
    post {
        always {
            emailext body: "${env.BUILD_URL}\b${currentBuild.absoluteUrl}",
                to: 'always@foo.bar',
                recipientProviders: [previous()],
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
        }
    }
}

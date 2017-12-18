pipeline {
    agent any
stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Staging'){
            steps {
                build job: 'PipelineDeployToStaging'
            }
            post{
                success{
                    echo 'Code deployed to Staging...'
                }
                failure{
                    echo 'Deployment to Staging failed...'
                }
            }
        }
    }
}
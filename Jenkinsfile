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
                    archiveArtifacts artifacts: '**/*.war'
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
        stage('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                build job: 'PipelineDeployToProd'
            }
            post{
                success{
                    echo 'Code deployed to Production...'
                }
                failure{
                    echo 'Deployment to Production failed...'
                }
            }
        }
    }
}
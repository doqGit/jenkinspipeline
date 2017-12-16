pipeline {
    agent any
stages{
        stage('Build'){
            steps {
                bat 'mvn clean PipelineAsCodeExample'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
    }
}
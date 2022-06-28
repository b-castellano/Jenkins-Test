pipeline {
    options {
        office365ConnectorWebhooks([
            [name: "Office 365",
            url: "https://uhgazure.webhook.office.com/webhookb2/ff9c60e4-9656-4149-9d93-bf7ed6a455d9@db05faca-c82a-4b9d-b9c5-0f64b6755421/JenkinsCI/7ee77d4cbc1d460a80c0cf8a61c38e51/561b3e4e-2928-4402-89cb-f289495ad51f",
            notifyBackToNormal: true, notifyFailure: true, notifyRepeatedFailure: true, notifySuccess: true, notifyAborted: true]
        ])
        buildDiscarder(
            logRotator(
                artifactDaysToKeepStr: '',
                artifactNumToKeepStr: '1',
                daysToKeepStr: '7',
                numToKeepStr: '10'
            )
        )
    }
    agent {
        docker {
            image 'maven:latest'
        }
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
            }
        }
        stage('test'){
            steps{
                echo 'testing'
            }
        }
        stage('sanity check'){
            steps{
                office365ConnectorSend webhookUrl:'https://uhgazure.webhook.office.com/webhookb2/ff9c60e4-9656-4149-9d93-bf7ed6a455d9@db05faca-c82a-4b9d-b9c5-0f64b6755421/JenkinsCI/7ee77d4cbc1d460a80c0cf8a61c38e51/561b3e4e-2928-4402-89cb-f289495ad51f',
                message:'Input requested', status:'sanity check'
                input 'Does everything look good?'
            }
        }
        stage('deploy'){
            steps{
                echo 'deploying'
            }
        }
    }
//     post {
//         always {
//         archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
//             junit 'build/reports/**/*.xml'
//         }
//     }
}
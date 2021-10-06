pipeline
{ 
    agent{
        docker{
            image 'mindbowser/android-30-sdk:1.0'
            args '-u root:root'
        }
    }
    stages{
        stage('Init')
        {
            steps {
                script {
                    lastCommitInfo = sh(script: "git log -1", returnStdout: true).trim()
                    commitContainsSkip = sh(script: "git log -1 | grep 'skip ci'", returnStatus: true)                    
                }
            }
        }
        stage('build')
        {
            steps{
                withCredentials([file(credentialsId: 'key_jks', variable: 'key_jks'), file(credentialsId: 'env_dev', variable: 'env_dev')]) {                    
                    sh "chmod +x gradlew"                    
                    sh "chmod +x Gemfile"
                    sh "cp \$key_jks ${workspace}/key.jks"
                    sh "cp \$env_dev ${workspace}/fastlane/.env.dev"
                    sh "fastlane build --env dev"
                }
            }
        }
        stage('slack notification')
        {
            steps{
                slackSend baseUrl: 'https://hooks.slack.com/services/',
                teamDomain: 'Notification_Hooks',
                channel: 'cicd',
                message: 'Release Build is successfully uploaded on Firebase  Distribution!!',
                tokenCredentialId: 'slack-cicd'                
            }
        }
    }
    post {
        always {            
            sh "chmod -R 777 ."
            deleteDir() 
        }
    }
}

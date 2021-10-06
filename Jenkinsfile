// slack_channel = 'android-ci-cd'

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
            //check git commit message contains "skip ci" if found don't run the pipeline
            steps {
                script {
                    lastCommitInfo = sh(script: "git log -1", returnStdout: true).trim()
                    commitContainsSkip = sh(script: "git log -1 | grep 'skip ci'", returnStatus: true)                    
                }
            }
        }
        stage('build')
        {
            // call fastlane lane for generate apk and uploading to testflight
            steps{
                withCredentials([file(credentialsId: 'key_jks', variable: 'key_jks'), file(credentialsId: 'env_dev', variable: 'env_dev')]) {
                    sh "ls -l ${workspace}"
                    sh "chmod +x gradlew"                    
                    sh "chmod +x Gemfile"
                    sh "cp \$key_jks ${workspace}/key.jks"
                    sh "cp \$env_dev ${workspace}/fastlane/.env.dev"
                    sh "fastlane build --env dev"    //eg. fastlane build --env development
                }
            }
        }
        stage('slack notification')
        {
            steps{
                slackSend channel: '#cicd', message: 'Welcome to Jenkins and slack', tokenCredentialId: 'slack-cicd', username: 'notificationhooks'
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

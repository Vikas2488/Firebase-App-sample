// pipeline {
//     agent { label 'dockerserver' } // if you don't have other steps, 'any' agent works
//     stages {
//         stage('Back-end') {
//             agent {
//                 docker {
//                   label 'dockerserver'  // both label and image
//                   image 'maven:3-alpine'
//                 }
//             }
//             steps {
//                 sh 'mvn --version'
//             }
//         }
//     }
// }
pipeline {
    agent { dockerfile true }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
                sh 'svn --version'
            }
        }
    }
}
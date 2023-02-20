pipeline {
    agent any
        options {
        disableConcurrentBuilds(abortPrevious: true)
    }

    
    stages {
        stage("Checkout Repo") {
            steps {
                sh '''
                echo 'Successfully executed Autocancel :  Pipeline Job'
                '''
            }
        }
        stage('Build') {
            steps {
                lock('build-lock') {
                    // This block will only be executed if the lock is acquired
                    echo 'Build started'
                    sleep 10 // Simulate a long build time
                    sh 'exit 1' // Simulate a build failure
                }
            }
        }        
//         stage("Timeout"){
//             steps{
//                 timeout(time: 10, unit: 'MINUTES') {
//                   input message: "does this look good"             
//             }
//         }
//      }
   }
    
    post {
        always {
            // Release the lock after the build completes
            releaseLock('build-lock')
        }
    }   
}

    

}


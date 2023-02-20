pipeline {
    agent any
        options {
        disableConcurrentBuilds(abortPrevious: true)
    }
    stages {
        stage('Pre-build check') {
            steps {
                script {
                    def lastBuild = currentBuild.rawBuild.getPreviousBuild()
                    if (lastBuild != null && lastBuild.result.isWorseThan(Result.SUCCESS)) {
                        error('The previous build failed. Cancelling the current build.')
                    }
                }
            }
        }
        // The rest of your pipeline stages go here

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
    post {
        always {
            milestone(1)
        }
        failure {
            input 'The previous build failed. Do you want to proceed with this build?'
        }
    }                

  }
}

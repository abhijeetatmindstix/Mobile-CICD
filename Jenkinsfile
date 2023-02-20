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
        
        stage('Build') {
            steps {
                sh 'exit 1' // Simulate a build failure
            }
        }
    }
    
    post {
        always {
            milestone(1)
        }
        failure {
            input 'The target branch is currently in a failed state. Do you want to continue'
        }
    }
}

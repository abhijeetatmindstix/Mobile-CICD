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
        stage("Timeout"){
            steps{
                timeout(time: 10, unit: 'MINUTES') {
                  input message: "does this look good"             
            }
        }
     }
   }
}

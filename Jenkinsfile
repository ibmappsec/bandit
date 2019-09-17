pipeline {
    agent any
    stages {
    stage('Pull code'){
      steps{
        echo 'downloading git directory..'
        git 'https://github.com/portantier/vulpy.git'
      }
    }
    stage('Install SAST tool'){
      steps{
        sh """
              virtualenv --no-site-packages .
              source bin/activate
              pip install bandit
              deactivate
              """
      }
    }
    stage('Run SAST scan') {
          steps {
              echo 'Testing insecure dependency'
              sh 'bandit -r ./bad'
          }
      }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}

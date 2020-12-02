pipeline {
  agent any
  stages {
    stage('Clone down') {
    }
    stage('Parallel execution') {
      parallel {
        stage('Say Hello') {
          steps {
            sh 'echo "hello world"'
          }
        }

        stage('buid app') {
          agent {
            docker {
              image 'gradle:jdk11'
            }

          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
            sh 'ls -l'
            deleteDir()
          }
        }

      }
    }

  }
}
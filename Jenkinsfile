pipeline {
  agent any
  stages {
    stage('clone down') {
      agent any
      steps {
        stash(name: 'code', excludes: '.git')
      }
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
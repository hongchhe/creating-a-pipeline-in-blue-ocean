pipeline {
  agent any
  stages {
    stage('stage_1') {
      steps {
        sh 'echo "good"'
      }
    }

    stage('stage_2') {
      parallel {
        stage('t1') {
          steps {
            echo 't1 branch run'
          }
        }

        stage('test') {
          steps {
            sleep 3
            sh 'echo $test_val'
          }
        }

      }
    }

    stage('end') {
      steps {
        echo 'End'
      }
    }

  }
  environment {
    test_val = '11'
  }
}
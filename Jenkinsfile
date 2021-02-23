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
            node(label: 'node_label_1') {
              echo 'node_label_1'
            }

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
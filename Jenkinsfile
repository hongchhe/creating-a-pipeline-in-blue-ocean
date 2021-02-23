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
            echo 't1 branch run';
            echo env;
            echo changeset;
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

    stage('Build') {
        when {
            anyOf {
                environment name: 'FORCE_DEPLOY', value: 'yes'
                environment name: 'BUILD_NUMBER', value: '1'
                changeset caseSensitive: true, pattern: '**/*'
            }
        }

        steps {
          echo env;
          echo changeset;
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
pipeline {
  agent any
  environment {
    TEST_VAL = '11'
    DISABLE_AUTH = 'true'
    DB_ENGINE    = 'sqlite'
  }

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
            sh 'printenv';
          }
        }

        stage('test') {
          steps {
            sleep 3
            sh 'echo $TEST_VAL'
          }
        }

        stage('print_env'){
          steps {
            echo sh(script: 'env|sort', returnStdout: true)
            echo sh(script: 'changeset', returnStdout: true)
          }
        }

      }
    }

    stage('Environment') {
        steps {
            echo "Database engine is ${DB_ENGINE}"
            echo "DISABLE_AUTH is ${DISABLE_AUTH}"
            sh 'printenv'
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
          echo "print the environment"
          echo env;
          echo changeset;
        }
    }

    stage('end') {
      steps {
        echo 'End'
      }
    }

  }

}
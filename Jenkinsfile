pipeline {
  agent any
  // agent {
  //   docker {
  //     image 'node:6-alpine' 
  //     args '-p 3000:3000' 
  //   }
  // }
  environment {
    TEST_VAL = '11'
    DISABLE_AUTH = 'true'
    DB_ENGINE    = 'sqlite'
  }


  }
  stages {
    stage('stage_1') {
      steps {
        sh '''
		       echo 'Hello, world!'
	      '''
        logstashSend failBuild: true, maxLines: 1000
      }
    }

    stage('stage_2') {
      parallel {
        stage('t1') {
          steps {
            echo 't1 branch run'
            sh 'printenv'
          }
        }

        stage('test') {
          steps {
            sleep 2
            sh 'echo $TEST_VAL'
          }
        }

        stage('print_env') {
          steps {
            echo sh(script: 'env|sort', returnStdout: true)
          }
        }

      }
    }

    // stage('Environment') {
    //     steps {
    //         echo "Database engine is ${DB_ENGINE}"
    //         echo "DISABLE_AUTH is ${DISABLE_AUTH}"
    //         sh 'printenv'
    //     }
    // }


    stage('Build') {
      when {
        anyOf {
          environment name: 'FORCE_DEPLOY', value: 'yes'
          environment name: 'BUILD_NUMBER', value: '1'
          changeset caseSensitive: true, pattern: '**/*'
        }

      steps {
        echo "print the environment";
        // echo sh(script: 'changeset', returnStdout: true)
        // sh 'npm install' 
      }

    }

    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('end') {
      steps {
        echo 'End'
      }
    }

  }
  environment {
    TEST_VAL = '11'
    DISABLE_AUTH = 'true'
    DB_ENGINE = 'sqlite'
  }
}
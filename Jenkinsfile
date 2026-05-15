pipeline {
    agent {
        node {
          label "linux && java21"
        }
      }

    stages {
        stage('Build') {
            steps {
                script {
                    for (int i = 0; i < 10; i++) {
                        echo("Script ${i}")
                    }
                }

                echo 'Hello Build'
                // sleep(5)
                // bat("mvn clean compile test-compile")
                echo 'Hello Build'
            }
        }
        stage('Test') {
            steps {
                echo 'Hello Test'
                // sleep(5)
                // bat("mvn test")
                echo 'Hello Test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Hello Deploy'
                sleep(5)
                echo 'Hello Deploy'
            }
        }
    }
    post {
    always {
      echo "I will always say Hello again!"
    }
    success {
      echo "Yay, success"
    }
    failure {
      echo "Oh no, failure"
    }
    cleanup {
      echo "Don't care success or error"
    }
  }
}
pipeline {
    agent none

    environment {
        AUTHOR = "Eko Kurniawan Khannedy"
        EMAIL = "echo.khannedy@gmail.com"
        WEB = "https://www.programmerzamannow.com"
    }

    stages {
        stage("Prepare") {

        environment {
            APP = credentials("parjo_secret")
        }

        agent {
            node {
            label "linux && java21"
            }
        }
        steps {
            echo("Author ${AUTHOR}")
            echo("Email ${EMAIL}")
            echo("Web ${WEB}")
            echo("Start Job : ${env.JOB_NAME}")
            echo("Start Build : ${env.BUILD_NUMBER}")
            echo("Branch Name : ${env.BRANCH_NAME}")
            echo("App User : ${APP_USR}")
            // echo("App Password : ${APP_PSW}")
            bat('echo "App Password : $APP_PSW" > "rahasia.txt"')
        }
        }
        stage('Build') {
            agent {
                node {
                label "linux && java21"
                }
            }
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
            agent {
                node {
                label "linux && java21"
                }
            }
            steps {
                script {
                    def data = [
                        "firstName": "Eko",
                        "lastName" : "Khannedy"
                    ]
                    writeJSON(file: "data.json", json: data)
                }

                echo 'Hello Test'
                // sleep(5)
                // bat("mvn test")
                echo 'Hello Test'
            }
        }
        stage('Deploy') {
            agent {
                node {
                label "linux && java21"
                }
            }
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
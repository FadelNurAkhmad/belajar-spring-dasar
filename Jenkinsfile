pipeline {
    agent none

    environment {
        AUTHOR = "Eko Kurniawan Khannedy"
        EMAIL = "echo.khannedy@gmail.com"
        WEB = "https://www.programmerzamannow.com"
    }

    //  triggers {
    //    cron("*/5 * * * *")
    //    pollSCM("H/5 * * * *")
    //    upstream(upstreamProjects: "job-1, job-2", threshold: hudson.model.Result.SUCCESS)
    //  }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }

    

    stages {
        stage("Preparation") {
            parallel {
                stage("Prepare Java") {
                agent {
                    node {
                    label "linux && java21"
                    }
                }
                steps {
                    echo("Prepare Java")
                    // sleep(5)
                }
                }
                stage("Prepare Maven") {
                agent {
                    node {
                    label "linux && java21"
                    }
                }
                steps {
                    echo("Prepare Maven")
                    // sleep(5)
                }
                }
            }
        }
        stage("Parameter") {
            agent {
                node {
                label "linux && java21"
                }
            }
            steps {
                echo "Hello ${params.NAME}"
                echo "You description is ${params.DESCRIPTION}"
                echo "Your social medis is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.SECRET}"
            }
        }
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
            // bat('echo "App Password : ${APP_PSW}" > "rahasia.txt"')
            bat("echo 'App Password : ${APP_PSW}' > 'rahasia.txt'")
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
            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "pzn,eko"
                parameters {
                choice(name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: "Which Environment?")
                }
            }
            agent {
                node {
                label "linux && java21"
                }
            }
            steps {
                echo("Deploy to ${TARGET_ENV}")
                // echo 'Hello Deploy'
                // sleep(5)
                // echo 'Hello Deploy'
            }
        }

        stage("Release") {
            when {
                expression {
                return params.DEPLOY
                }
            }
            agent {
                node {
                label "linux && java21"
                }
            }
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "parjo_secret",
                    usernameVariable: "USER",
                    passwordVariable: "PASSWORD"
                )]) {
                bat('echo "Release it with -u $USER -p $PASSWORD" > "release.txt"')
                }
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
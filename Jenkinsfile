pipeline {
    agent any

    stages {
        stage('install-pip-deps') {
            steps {
                script {
                    build()
                }
            }
        }
        stage('deploy-to-dev') {
            steps {
                script {
                    deploy("dev", 7001)
                }
            }
        }
        stage('tests-on-dev') {
            steps {
                script {
                    test("dev")
                }
            }
        }
        stage('deploy-to-stg') {
            steps {
                script {
                    deploy("stg", 7002)
                }
            }
        }
        stage('tests-on-stg') {
            steps {
                script {
                    test("stg")
                }
            }
        }
        stage('deploy-to-preprod') {
            steps {
                script {
                    deploy("preprod", 7003)
                }
            }
        }
        stage('tests-on-preprod') {
            steps {
                script {
                    test("preprod")
                }
            }
        }
        stage('deploy-to-prod') {
            steps {
                script {
                    deploy("prod", 7004)
                }
            }
        }
        stage('tests-on-prod') {
            steps {
                script {
                    test("prod")
                }
            }
        }
    }
}


def build() {
    echo "Branching python greetings.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "dir"
    echo "Creating enviroment.."
    bat "venv\\Scripts\\python.exe -m venv venv"
    echo "Installing dependecies.."
    bat "venv\\Scripts\\python.exe -m pip install -r requirements.txt"
}

def deploy(String environment, int port) {
}

def test(String environment) {
}
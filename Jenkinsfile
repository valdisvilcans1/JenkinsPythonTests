pipeline {
    agent any
    triggers { 
        pollSCM('*/1 * * * *') 
    }
    stages {
        stage('install-pip-deps') {
            steps {
                echo "Installing pip dependecies.."
                script {
                    build()
                }
            }
        }
        stage('deploy-to-dev') {
            steps {
                script {
                    deploy("DEV", 1010)
                }
            }
        }
        stage('tests-on-dev') {
            steps {
                script {
                    test("DEV")
                }
            }
        }
        stage('deploy-to-stg') {
            steps {
                script {
                    deploy("STG", 2020)
                }
            }
        }
        stage('tests-on-stg') {
            steps {
                script {
                    test("STG")
                }
            }
        }
        stage('deploy-to-preprod') {
            steps {
                script {
                    deploy("PRD", 3030)
                }
            }
        }
        stage('tests-on-preprod') {
            steps {
                script {
                    test("PRD")
                }
            }
        }
        stage('deploy-to-prod') {
            steps {
                script {
                    test("PRD")
                }
            }
        }
        stage('tests-on-prod') {
            steps {
                script {
                    test("PRD")
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
    bat "py -m venv venv"
    echo "Installing dependecies.."
    bat "./venv/bin/python -m pip install -r requirements.txt "
}

def deploy(String environment, int port) {

}

def test(String environment) {

}
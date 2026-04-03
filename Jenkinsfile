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
                    deploy("DEV", 7001)
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
                    deploy("STG", 7002)
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
                    deploy("PRE", 7003)
                }
            }
        }
        stage('tests-on-preprod') {
            steps {
                script {
                    test("PRE")
                }
            }
        }
        stage('deploy-to-prod') {
            steps {
                script {
                    deploy("PRD", 7004)
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
    bat "venv\\Scripts\\python.exe -m pip install -r requirements.txt "
}

def deploy(String environment, int port) {
    echo "Branching python greetings.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "npm install pm2"
    bat "node_modules\\.bin\\pm2 delete greetings-app-${environment} || exit 0"
    bat "node_modules\\.bin\\pm2 start -n greetings-app-${environment} app.py -- ${port}"
}

def test(String environment) {
    echo "Branching js framework course.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'
    
}
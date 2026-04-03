// GitHub: https://github.com/valdisvilcans1/JenkinsPythonTests/tree/main

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


def branch_python_greetings() {
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
}


def build() {
    echo "Installing all necessary node dependencies.."
    branch_python_greetings()
    bat "dir"
    echo "Creating enviroment.."
    bat "venv\\Scripts\\python.exe -m venv venv"
    echo "Installing dependecies.."
    bat "venv\\Scripts\\python.exe -m pip install -r requirements.txt"
}

def deploy(String environment, int port) {
    echo "Deployment to ${environment} environment has started.."
    branch_python_greetings()
    echo "Installing pm2 dependecy.."
    bat "npm install pm2"
    echo "Deleting old connection.."
    bat "node_modules\\.bin\\pm2 delete greetings-app-${environment} || exit 0"
    echo "Starting new connection.."
    bat "node_modules\\.bin\\pm2 start -n greetings-app-${environment} app.py --interpreter %CD%\\venv\\Scripts\\pythonw.exe -- --port ${port}"
}

def test(String environment) {
    echo "Testing application service has started on ${environment} environment.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'
    echo "Installing all npm dependencies.."
    bat "npm install"
    echo "Running npm greetings skript.."
    bat "npm run greetings greetings_${environment}"
}
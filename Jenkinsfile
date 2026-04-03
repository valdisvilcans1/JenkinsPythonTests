pipeline {
    agent any
    triggers { 
        pollSCM('*/1 * * * *') 
    }
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
    echo "Branching python greetings.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
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
    bat "dir"
    bat "node_modules\\.bin\\pm2 delete greetings-app-${environment} || exit 0"
    bat "node_modules\\.bin\\pm2 start app.py --name greetings-app-${environment} --interpreter venv\\Scripts\\python -- --port ${port}"
}

def test(String environment) {
    echo "Branching js framework course.."
    git branch: 'main', poll: true, url: 'https://github.com/mtararujs/course-js-api-framework.git'
    echo "Installing npm dependencies.."
    bat "npm install"
    echo "Running greetings.."
    bat "npm run greetings greetings_${environment}"
}
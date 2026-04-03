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

def build() {
    echo "Installing all necessary python and node dependencies.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "dir"
    echo "Creating enviroment.."
    bat "py -m venv venv"
    echo "Installing dependecies.."
    bat "venv\\Scripts\\python.exe -m pip install -r requirements.txt "
    echo "Installing pm2 package.."
    bat "npm install pm2"
}

def deploy(String environment, int port) {
    echo "Deployment to ${environment} environment has started.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "node_modules\\.bin\\pm2 delete greetings-app-${environment} || exit 0"
    bat "node_modules\\.bin\\pm2 start -n greetings-app-${environment} app.py -- ${port}"
}

def test(String environment) {
    echo "Testing Sample Book Application service has started on ${environment} environment.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'
    echo "Installing npm dependencies.."
    bat "npm install"
    echo "Running greetings.."
    bat "npm run greetings greetings_${environment}"
}
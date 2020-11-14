def envs = []
pipeline {
    agent any
    stages {
        stage('Demo pipeline'){
            steps {
                echo "Build number is $BUILD_NUMBER"
                script{
                    my_func('TEST')
                }

            }
        }

        stage('Env'){
            steps {
                echo "Envs"
                script {
                    envs = ['a', 'b', 'c']
                }
            }
            
        }

        stage('parallel stage') {
            steps {
                script {

                        def apps = [:]
                        envs.each {
                            performDeploymentStages(it)
                        }
                        parallel apps
                }
            }
        }
    }
}

def performDeploymentStages(String app) {
    stage("build ${app}") {
        echo "Building the app [${app}] on node [a]"
    }
    stage("deploy ${app}") {
        echo "Deploying the app ${app}] on node [b]"
    }
}

def my_func(var){
    println(var)
}

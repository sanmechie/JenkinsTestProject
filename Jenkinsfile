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
        stage('Deploy and Integration tests') {
            when {
                expression {
                  return !envs.isEmpty()
                }
            }
            steps {
               script{
                envs.each{
                    env ->
                    deploys[env] = {
                        echo "Hi ${env}"
                    }
                }
                parallel deploys
               }
            }
        }
    }



}

def my_func(var){
    println(var)
}

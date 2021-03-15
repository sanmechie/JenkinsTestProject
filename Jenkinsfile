def envs = []
def val

pipeline {
    agent none
    stages {
        stage('Demo pipeline'){
            agent any
            steps {
                echo "Build number is $BUILD_NUMBER"
                script{
                    echo "Hi"
                }

            }
        }

        stage('Env'){
            agent any
            steps {
                echo "Envs"
                script {
                    envs = 'a, b, c'
                }
            }
            
        }

        stage('Dynamic Building') {
        agent {
                        docker {
            image 'mcr.microsoft.com/dotnet/core/sdk:3.1.101'
        }
        }
              steps {
                executeModuleScripts('build') // local method, see at the end of this script
              }
            }
    }
}


void executeModuleScripts(String operation) {

          def allModules = ['module1', 'module2', 'module3', 'module4', 'module11']

          allModules.each { module ->  
        

            // here is the trick           
            script {
              stage(module) {

                  }
               steps{
                  script {
                    running_set = [:]
                        envs.tokenize(',').each {
                            running_set[it] = {my_func(it)}
                        }
                        parallel(running_set)
                }
               }
              }
            }
          }

}

def my_func(var){
    println(var)
}
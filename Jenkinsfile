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
                    my_func('TEST')
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
                  agent any
               steps{
                   echo "${module}"
               }
              }
            }
          }

}
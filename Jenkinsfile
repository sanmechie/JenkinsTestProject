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
        stage('paralel stage'){
            parallel{
                    stage('Dynamic Building') {
                    agent any
                    steps {
                        executeModuleScripts() // local method, see at the end of this script
                    }
            }

            }
        }

    }
}
def my_func(var){
    for (int i=0; i<=100; i++){
        println(i)
    }
}


void executeModuleScripts() {
    running_set1 = [

    'b1': {
        my_func('a')
    },
    'b2': {
        my_func('b')
    }

    ]
running_set2= [
    'a1': {
        my_func('1')
    },
    'a2': {
        my_func('2')
    }

]

          def allModules = [{running_set1}, {running_set2}]

          allModules.each { module ->  
        

            // here is the trick           
            script {
              stage(module) {
                        script{
                            steps{
                                parallel(module)
                            }
                        }

                  }

              }
            }
          }


def envs = []
def val

def my_func(var){
    for (int i=0; i<=100; i++){
        println(i)
    }
}
running_set1 = [

    'a': {
        my_func('a')
    },
    'b': {
        my_func('b')
    }

]

running_set2 = [

    '1': {
        my_func('1')
    },
    '2': {
        my_func('2')
    }

]

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


void executeModuleScripts() {

          def allModules = [running_set1, running_set2]

          allModules.each { module ->  
        

            // here is the trick           
            script {
              stage(module) {
                        parallel(module)

                  }

              }
            }
          }

def envs = []
def val

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
                    envs = 'a, b, c'
                }
            }
            
        }

        stage('parallel stage') {
            steps {
                
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

// def performDeploymentStages(String app) {
//     stage("build ${app}") {
//         echo "Building the app [${app}] on node [a]"
//         script{
//             my_func2()
//         }
//     }
//     stage("deploy ${app}") {
//         if (val > 5) {
//         echo "Deploying the app ${app}] on node [b]"
//     }
//     }
// }


def my_func(var){
    def flag = false
    stage("Deplo and Test ${var}"){

        try {
            echo "Deploying ${var}"

            flag = true
            x

        } catch (Exception e){
            flag = false
            unstable("Deploy Failed ${var}")
        }

        if (flag){
            try {
        echo "Testing ${var}"
            flag = true

        } catch (Exception e){
            unstable("Test Failed ${var}")
        }
        }

    }

        
    
}


def my_func2(){
   Random ran = new Random()
   val = ran.nextInt(5)
   return val
}

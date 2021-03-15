def envs = []
def val
import java.time.*


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
    for (int i=0; i<=var; i++){
        println(i)
    }
}


void executeModuleScripts() {
    running_set1 = [

    'b1': {
        my_func(10)
    },
    'b2': {
        my_func(20)
    }

    ]
running_set2= [
    'a1': {
        my_func(30)
    },
    'a2': {
        my_func(40)
    }

]

char[] chars = "abcdefghijklmnopqrstuvwxyz".toCharArray();
StringBuilder sb = new StringBuilder(20);
Random random = new Random();
for (int i = 0; i < 20; i++) {
    char c = chars[random.nextInt(chars.length)];
    sb.append(c);
}
String output = sb.toString();
System.out.println(output);

          def allModules = [running_set1, running_set2]

          allModules.each { module ->  
          

            // here is the trick           
            script {
              stage(output) {
                                                       LocalDateTime t = LocalDateTime.now();
                            print(t)
                                parallel(module)
 

                  }

              }
            }
          }


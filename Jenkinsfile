pipeline {
    agent any
    stages {
        stage('Demo pipeline'){
            steps {
                echo "Build number is $BUILD_NUMBER"
                script{
                    my_func(TEST)
                }

            }
        }
    }

    environment {
        
        TEST = '1'
    }

}


def my_func(my_var){
        println(my_var)
    }
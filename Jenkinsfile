pipeline {
    agent any
    stages {
        stage{'Demo pipeline'}{
            echo "Build number is $BUILD_NUMBER"
            steps {
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
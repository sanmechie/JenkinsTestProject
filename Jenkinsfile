def jobs         = [:]


def my_func(var){
    for (int i=0; i < var; i++){
        println(i)
    }
}

modules.each {module ->

running_set1 = [

    'india': {
        my_func(10)
    },

    'Kar': {
        my_func(20)
    },

]

running_set2 = [

    'india': {
        my_func(30)
    },

    'Kar': {
        my_func(40)
    },

]

def modules = [running_set1, running_set2]
modules.each {module ->
char[] chars = "abcdefghijklmnopqrstuvwxyz".toCharArray();
StringBuilder sb = new StringBuilder(20);
Random random = new Random();
for (int i = 0; i < 20; i++) {
    char c = chars[random.nextInt(chars.length)];
    sb.append(c);
}
String output = sb.toString();
System.out.println(output);

    jobs["jobs-${output}"] = {
        node {
            stage("Build ${output}") {
                build job: parallel(module)
            }
        }
    }

}



pipeline {
    agent none
    stages {
        stage('Build apps(s)') {
            steps {
                script {
                    parallel jobs
                }
            }
        }
    }
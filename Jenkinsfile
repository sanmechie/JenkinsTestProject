def jobs   = [:]

def running_set1 = [

    'UK': {
        my_func(10)
    },

    'Lon': {
        my_func(20)
    },

]

def running_set2 = [

    'india': {
        my_func(30)
    },

    'Kar': {
        my_func(40)
    },

]

def my_func(var){
    print(var)
}

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
               def my = module
                build job: parallel(my)
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
                try{
                 catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
                 parallel jobs
                 }
                }
                catch(err){
                    println('Ignore this error')
                }
            }
        }
    }
}
}
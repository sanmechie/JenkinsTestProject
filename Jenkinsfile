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
for (int j=0; j<modules.size(); j++){
def module = modules[j]
println(module)
char[] chars = "abcdefghijklmnopqrstuvwxyz".toCharArray();
StringBuilder sb = new StringBuilder(20);
Random random = new Random();
for (int i = 0; i < 20; i++) {
    char c = chars[random.nextInt(chars.length)];
    sb.append(c);
}
String output = sb.toString();
System.out.println(output);

    jobs["jobs-${j}"] = {
      
            
            stage("Build ${j}") {
           script{
               println(module)
                parallel(module)
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

                 parallel(jobs)

                }
                catch(err){
                    println(err)
                }
            }
        }
    }
}
}
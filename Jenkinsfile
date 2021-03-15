


pipeline {
    agent none
stages {
     stage('Start Pipeline') {
        steps {
            script {
                sh "echo HELLO moto razr!"
            }
        }  
     }

    stage('Initializing Parallel Dynamic Stages'){
        steps {
            script {
                // Run all Nth step for all Projects in Parallel. 
                buildStages.each { bs -> parallel(bs) }


                // OR uncomment the following code (if conditional on boolean variable).
                /*
                for (builds in buildStages) {
                    if (runParallel) {
                        parallel(builds)
                    } else {
                        // run serially (nb. Map is unordered! )
                        for (build in builds.values()) {
                            build.call()
                        }
                    }
                }
                */        

            }   
        }
     } 

    stage('Done') {
        steps{
        echo "Done"
    }   
    }   
}
}

def prepareOneBuildStage(String name) {
  def proj_name = name.split(' ')[0]
  def proj_parallel_sub_step = name.split(' ')[1]
  // return the whole chunkoni (i.e. for a given stage) - will be named dynamically.
  return {
    stage("BUILD Project-${proj_name} Parallel_Step_${proj_parallel_sub_step}") {
      println("Parallel_Step # ${proj_parallel_sub_step} of Project => ${proj_name}")
      sh(script:"echo \"Parallel_Step # ${proj_parallel_sub_step} of Project => ${proj_name}\" && sleep 20", returnStatus:true)
      // -- OR -- you can call Gradle task i.e. rpm / any other / any other command here. 
    }
  }
}

// Set up List<Map<String,Closure>> describing the builds. section now.
buildStages = prepareBuildStages()
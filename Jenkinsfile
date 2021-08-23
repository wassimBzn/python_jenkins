pipeline {
 agent none
 stages {

  stage("parallel") {
       
     parallel {
       stage("Build") {
         agent {
           label  "slave"
         }
         steps {
          git branch: 'main', url: 'https://github.com/wassimBzn/python_jenkins.git'
          bat 'build.bat'
         }
       }
       stage("Test") {
          agent {
           label  'slave'
          }
         steps {
          bat 'test.bat'
         }
        }
     }
  }

  stage("Non parallel"){
    agent {
      label  "master"
    }
 
      steps {
       git branch: 'main', url: 'https://github.com/wassimBzn/python_jenkins.git'
       bat 'deploy.bat'
 
    }
  }
 

}
 post {
    always {
     echo "always runs regardless of the completion status of the Pipeline run"
    }
    success {
    echo  "step will run only if the build is successful"
    }
    failure {
    echo "only when the Pipeline is currently in a   state run, usually expressed in the Web UI with the red indicator."
    }
    unstable {
    echo  "current Pipeline has   state, usually by a failed test, code violations and other causes, in order to run. Usually represented in a web UI with a yellow indication."
    }
    changed {
    echo  "can only be run if the current Pipeline is running at a different state than the previously completed Pipeline"
    }
  }

}  
   

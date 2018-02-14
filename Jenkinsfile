/* this is working DSL in windows with pipline maven integration plugin -- if didnt work try removing <settings> tag in nexuscongi
pipeline {
    agent any
    stages {
        stage ('Compile Stage') {
            steps {
                withMaven(maven : 'apache-maven-3.3.9') {
                    bat 'mvn -s nexusconfigurations/nexus.xml clean compile'
                }
            }
        }
        stage ('Testing Stage') {
            steps {
                withMaven(maven : 'apache-maven-3.3.9') {
                    bat 'mvn -s nexusconfigurations/nexus.xml test'
                }
            }
        }
        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'apache-maven-3.3.9') {
                    bat 'mvn -s nexusconfigurations/nexus.xml deploy'
                }
            }
        }
    }
}
*/

/*testing in openshift jenkins - not able to download artifacts from maven central..failed in last step
pipeline {
    agent {
              label 'maven'
            }
    stages {
        stage ('Compile Stage') {
            steps {
                 
                    sh "mvn -s nexusconfigurations/nexus.xml clean compile"
               
            }
        }
        stage ('Testing Stage') {
            steps {
                 
                    sh "mvn -s nexusconfigurations/nexus.xml test"
                
            }
        }
        stage ('Deployment Stage') {
            steps {
                 
                    sh "mvn -s nexusconfigurations/nexus.xml deploy"
                
            }
        }
    }
}
*/


// this is working DSL in windows with pipline maven integration plugin -- if didnt work try removing <settings> tag in nexuscongi --
// deploy to openshift
pipeline {
 agent any

 stages {
  stage('Compile Stage') {

   steps {
    withMaven(maven: 'apache-maven-3.3.9') {
     bat 'mvn -s nexusconfigurations/nexus.xml clean compile'
    }
   }
  }

  stage('Testing Stage') {

   steps {
    withMaven(maven: 'apache-maven-3.3.9') {
     bat 'mvn -s nexusconfigurations/nexus.xml test'
    }
   }
  }


  stage('Deployment Stage') {
   steps {
    withMaven(maven: 'apache-maven-3.3.9') {
     bat 'mvn -s nexusconfigurations/nexus.xml deploy'
    }
   }
  }

  stage('Archive jar to Jenkins target') {

   steps {
    withMaven(maven: 'apache-maven-3.3.9') {
     archive 'target/*.jar'
    }
   }
  }



  stage('Approve to Deploy on Openshift') {
   steps {
    timeout(time: 2, unit: 'DAYS') {
     input message: 'Do you want to Approve?'
    }
   }
  }
  stage('login') {
   steps {
    sh 'oc login https://192.168.99.100:8443 --token=G2AsDzhLjmwyBsRCYmRu0EekAGGetQlFJewtR2XmyVA --insecure-skip-tls-verify'
   }
  }
  stage('new project') {
   steps {
    sh 'oc new-project jdk71'
   }
  }
  stage('new build') {
   steps {
    sh 'oc new-build --name=abc redhat-openjdk18-openshift --binary=true'
   }
  }
  stage('build') {
   steps {
    sh "rm -rf oc-build && mkdir -p oc-build/deployments"
    sh "cp target/student-services-0.0.1-SNAPSHOT.jar oc-build/deployments/ROOT.jar"

    sh 'oc start-build abc --from-dir=oc-build --wait=true  --follow'

    //mv /path/to/file.old /path/to/file.new
    /*sh "cd target && mv student-services-0.0.1-SNAPSHOT.jar ROOT.jar"
    sh "cd target && mkdir deployments"
    sh "cp target/ROOT.jar deployments"
    sh 'oc start-build abc --from-dir=target/deployments  --follow' */


   }
  }
  stage('deploy expose') {
   steps {
    sh 'oc new-app abc'
    sh 'oc expose svc/abc'
   }
  }
  stage('scaling') {
   steps {
    sh ' oc scale --replicas=10 dc abc'
   }
  }

 }
}
/*
stage ('buildInDevelopment'){
steps{
openshiftBuild(namespace: 'jenkinsfdeploy', bldCfg: 'php', showBuildLogs: 'true')}}

stage ('deployInDevelopment'){
steps{
openshiftDeploy(namespace: 'jenkinsfdeploy', depCfg: 'php')
openshiftScale(namespace: 'jenkinsfdeploy', depCfg: 'php',replicaCount: '2')}}*/

/*
//testing oc cli
stage('Create Image Builder') {
                when {
                  expression {
                    openshift.withCluster('https://192.168.99.100:8443, QF03ylfGRGhSR24vxmCU7OXhUVx3k9RAZTnbT4gjncw') {
                      openshift.withProject('abc') {
                        return !openshift.selector("bc", "tasks").exists();
                      }
                    }
                  }
                }
                steps {
                  script {
                    openshift.withCluster('https://192.168.99.100:8443, QF03ylfGRGhSR24vxmCU7OXhUVx3k9RAZTnbT4gjncw') {
                      openshift.withProject('abc')  {
                        openshift.newBuild("--name=tasks", "--image-stream=jboss-eap70-openshift:1.5", "--binary=true")
                      }
                    }
                  }
                }
              }
              stage('Build Image') {
                steps {
                  sh "rm -rf oc-build && mkdir -p oc-build/deployments"
                  sh "cp target/openshift-tasks.war oc-build/deployments/ROOT.war"
                  
                  script {
                    openshift.withCluster('https://192.168.99.100:8443, QF03ylfGRGhSR24vxmCU7OXhUVx3k9RAZTnbT4gjncw') {
                      openshift.withProject('abc')  {
                        openshift.selector("bc", "tasks").startBuild("--from-dir=oc-build", "--wait=true")
                      }
                    }
                  }
                }
              }


    }
}*/
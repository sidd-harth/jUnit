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
		
		 stage ('Archive jar to Jenkins target') {

            steps {
                withMaven(maven : 'apache-maven-3.3.9') {
                    archive 'target/*.jar'
                }
            }}
			
			
			
			stage('Approve to Deploy on Openshift') {
					steps {
					timeout(time: 2, unit: 'DAYS') {
						input message: 'Do you want to Approve?'
					}}
				}
				stage('login'){
	        steps{
	        sh 'oc login https://192.168.99.100:8443 --token=G2AsDzhLjmwyBsRCYmRu0EekAGGetQlFJewtR2XmyVA --insecure-skip-tls-verify'
	        }
	    }
	    stage('new project'){
	        steps{
	        sh 'oc new-project jdk62'
	        }
	    }
	    stage('new build'){
	        steps{
	        sh 'oc new-build --name=abc redhat-openjdk18-openshift --binary=true'
	        }
	    }	 
	    stage( build'){
	        steps{
			sh "rm -rf oc-build && mkdir -p oc-build/deployments"
            sh "cp target/student-services-0.0.1-SNAPSHOT.jar oc-build/deployments/ROOT.war"
	        //sh 'oc start-build abc --from-repo=http://localhost:8081/#browse/browse:testRepo:com%2Fin28minutes%2Fspringboot%2Fstudent-//services%2F0.0.1-20180213.202051-5%2Fstudent-services-0.0.1-20180213.202051-5.jar --follow'
	        }
	    }
			    stage(start build'){
	        steps{
			sh 'oc start-build' abc --follow
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
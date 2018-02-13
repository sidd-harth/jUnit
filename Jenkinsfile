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

stage ('buildInDevelopment'){
steps{
openshiftBuild(namespace: 'jenkinsfdeploy', bldCfg: 'php', showBuildLogs: 'true')}}

stage ('deployInDevelopment'){
steps{
openshiftDeploy(namespace: 'jenkinsfdeploy', depCfg: 'php')
openshiftScale(namespace: 'jenkinsfdeploy', depCfg: 'php',replicaCount: '2')}}

    }
}
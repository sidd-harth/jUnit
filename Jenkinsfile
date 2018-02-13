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

stage ('buildInDevelopment'){
steps{
openshiftBuild(namespace: 'jenkinsfdeploy', buildConfig: 'php', showBuildLogs: 'true')}}

stage ('deployInDevelopment'){
steps{
openshiftDeploy(namespace: 'jenkinsfdeploy', deploymentConfig: 'php')
openshiftScale(namespace: 'jenkinsfdeploy', deploymentConfig: 'php',replicaCount: '2')}}

    }
}

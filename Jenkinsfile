/* this is working DSL in windows with pipline maven integration plugin
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

/*testing in openshift jenkins*/
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
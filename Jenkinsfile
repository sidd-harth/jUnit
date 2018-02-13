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

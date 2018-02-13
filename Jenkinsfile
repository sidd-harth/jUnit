def mvnCmd = "mvn -s nexusconfigurations/nexus.xml"

pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'apache-maven-3.3.9') {
                    bat '${mvnCmd} clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'apache-maven-3.3.9') {
                    bat '${mvnCmd} test'
                }
            }
        }


        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'apache-maven-3.3.9') {
                    bat '${mvnCmd} deploy'
                }
            }
        }
    }
}

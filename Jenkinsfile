import groovy.json.JsonSlurper;
  
properties([[$class: 'GitLabConnectionProperty', gitLabConnection: 'my-gitlab-connection']])
 
node{
    stage 'Build, Test and Package'
    env.PATH = "${tool 'maven'}/bin:${env.PATH}"
    checkout scm
    
    withMaven(
                maven: 'maven',
               // mavenSettingsConfig: 'a1adf035-653b-410d-b5a6-16b6da77b322',
                mavenLocalRepo: '.repository') {
     
            // Run the maven build
            sh "mvn clean package "
        }
}

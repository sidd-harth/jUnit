node(maven) {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
       sh 'mvn clean package'

    }
}

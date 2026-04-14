pipeline {
    agent {
       docker {
          image 'maven:3.9.5-amazoncorretto-17'
       }
    }

    stages {
        stage('Git') {
            steps {
               git branch: 'main', changelog: false, poll: false, url: 'https://codeberg.org/argonaultes-epsi-paris/epsi-paris-i1-icde848.git'
            }
        }
        stage("Test") {
            steps {
                sh 'mvn test'
                archiveArtefacts artifacts: "target/*.jar", fingerprint: true,
                followSymLinks: false
            }
        }
    }
}
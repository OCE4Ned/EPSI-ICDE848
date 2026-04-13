pipeline {
    agent {
       docker {
          image 'maven:3.9.5-amazoncorretto-17'
       }
    }

    stages {
        stage('Git') {
            steps {
               git branch: 'main', credentialsId: 'b231144f-1d23-45ba-9005-633d5350d9eb', url: 'https://github.com/OCE4Ned/EPSI-ICDE848.git'
            }
        }
        stage("Maven test") {
            steps {
                sh 'mvn test'
            }
        }
    }
}
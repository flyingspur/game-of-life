node {
        stage("Main build") {

            checkout scm

            docker.image('mzagar/jenkins-slave-jdk-maven-git').inside {

              stage("Hostname") {
                sh "hostname"
              }

              stage("Build") {
                sh "mvn install"
              }

              stage("Hostname") {
                sh "hostname"
              }

           }

        }
}


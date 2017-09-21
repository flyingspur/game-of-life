node {
        stage("Main build") {

            checkout scm

            docker.image('mzagar/jenkins-slave-jdk-maven-git').inside {

              stage("Build") {
                sh "mvn install"
              }

           }

        }
}

node {
		def server = Artifactory.server 'ART'
		//If Artifactory is not defined inside Jenkins configuration
		//def server = Artifactory.newServer url: SERVER_URL, credentialsId: CREDENTIALS
		def rtMaven = Artifactory.newMavenBuild()
		def buildInfo
		// stage("Main build") {

		// checkout scm

		docker.image('mzagar/jenkins-slave-jdk-maven-git').inside {
	
			stage("Checking out code") {
				checkout scm
			}

			stage("Hostname") {
				sh "hostname"
			}

			stage ('Artifactory configuration') {
				rtMaven.tool = MAVEN_TOOL // Tool name from Jenkins configuration
				rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
				rtMaven.resolver releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot', server: server
				buildInfo = Artifactory.newBuildInfo()
			}

			//stage("Maven Build") {
			//	sh "mvn install"
			//}

			stage ('Exec Maven') {
				rtMaven.run pom: 'pom.xml', goals: 'install', buildInfo: buildInfo
			}

			stage ('Publish build info') {
				server.publishBuildInfo buildInfo
			}

		}

	}
}

pipeline{
	agent any
	tools{
		maven 'localMaven'
	}
	stages{
		stage('Build'){
			steps{
				echo "Starting the build process"
				sh "mvn clean package"
			}
			post{
				success{
					echo "Now Archiving..."
					archiveArtifacts artifacts: "**/target/*.war"
				}
			}
		}
	}
}
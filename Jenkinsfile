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

		stage('Deploy to Stage'){
			steps{
				echo "Starting the deployment to staging server"
				build job: 'deploy-to-container-apache'
			}
		}

		stage('Deploy to Production'){
			steps{
				echo "Waiting for the production deployment approval?"
				timeout(time:5 ,units:'DAYS'){
					input message: "Approve Production Deployment?"
				}

				echo "Starting the deployment to production ..."
				build job: "deploy-to-production"
			}
			post{
				success{
					echo "Deployed to production successfully"
				}

				failure{
					echo "Deployment Failed"
				}
			}
		}
	}
}
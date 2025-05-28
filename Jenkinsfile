pipeline{
	agent any
	environment {
		LANG='en_US.UTF-8'
		LC_ALL='en_US.UTF-8'
	}
	tools{
		maven 'Maven'
	}
	
	stages {
		stage('Checkout'){
			steps{
				git branch : 'main' , url : 'https://github.com/ayushRajar/MavenWebApp.git'
			}
		}
		
		stage('Build') {
			steps {
				sh 'mvn clean install'
			}
		}
		
		stage('Achieve') {
			steps{
				achieveArtifacts artifacts : 'target/*.war', fingerprint:true
			}
		}
		stage('Deploy'){
			steps{
				sh 'ansible-playbook ansible/playbook.yml -i ansible/host.ini'
			}
		}
	}
	post{
		success {
			echo 'Deployed Successfully'
		}
		
		failure {
			echo 'Deployment Failed'
		}
	}
}
		

pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git branch: 'main', url: 'https://github.com/TanZhiYu98/SimpleWebApp.git'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
			}
		}
    		stage('UI Test'){
      			steps {
        			echo 'UI Test'
      			}
    		}
		stage('SonarQube'){
			steps {
				withSonarQubeEnv('My SonarQube Server') {
				sh 'mvn clean package sonar:sonar'
			      }
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}

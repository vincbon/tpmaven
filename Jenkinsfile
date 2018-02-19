pipeline {
	agent any
	stages {
	    stage('SonarQube analysis') {
            steps {
                sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar -Dsonar.host.url=\"${SONAR_HOST_URL}\" -Dsonar.login=\"${SONAR_LOGIN}\""
            }
        }
		stage('Build') {
			steps {
				sh 'mvn -B -DskipTests clean package'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			}
			post {
				always {
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
		stage('Archive') {
			steps {
				archiveArtifacts(artifacts: 'target/')
			}
		}
	}
}

pipeline {
    agent {label 'WindowsSlave'}

    stages {
        stage ('Git Fetch Stage') {
            steps{
                git credentialsId: 'bd97a44a-e6f1-4982-98f4-cd71e2067884', url: 'git@code.siemens.com:mytestprojectsgroup/maventestproject.git'
            }
        }
        stage ('Compile Stage') {
            steps{
                bat "mvn clean compile"
            }
        }
        stage ('Test Stage'){
	        parallel{
		        stage('Test Compile Stage'){
			        steps{
					    bat 'mvn test-compile'
			        }
		        }
		        stage('Test Cases Stage'){
			        steps{
					    bat 'mvn test'
			        }
		        }
	        }
        }
        stage ('Build Stage'){
            steps{
                bat 'mvn install'
            }
        }
        stage ('SonarQube Analysis Stage'){
            steps{
                bat 'mvn sonar:sonar -Dsonar.host.url=http://inakr06958wspr.ad001.siemens.net:9000 -Dsonar.login=admin -Dsonar.password=moladmin -Dsonar.projectKey=testing.jenkins.slave -Dsonar.projectName="Jenkins Slave Test" -Dsonar.projectVersion=2.0'
            }
        }
    }
}

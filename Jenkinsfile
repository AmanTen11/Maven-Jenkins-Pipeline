pipeline {
    agent any

    stages {
        stage ('Git Fetch Stage') {
            steps{
                echo "Git Stage"
            }
        }
        stage ('Compile Stage') {
            steps{
			    echo "Compile Stage"
                //sh "mvn clean compile"
            }
        }
        stage ('Test Stage'){
	        parallel{
		        stage('Test Compile Stage'){
			        steps{
					    echo "Compile Stage in Paralle;"
					    //sh 'mvn test-compile'
			        }
		        }
		        stage('Test Cases Stage'){
			        steps{
						echo "Test Case Stage in Parallel"
					    //sh 'mvn test'
			        }
		        }
	        }
        }
        stage ('Build Stage'){
            steps{
				echo "Build Stage"
                //sh 'mvn install'
            }
        }
        stage ('SonarQube Analysis Stage'){
            steps{
				echo "SonarQube Stage"
            }
        }
    }
}

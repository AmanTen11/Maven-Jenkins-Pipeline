pipeline {
    agent any
    
    tools{
        maven "Java_Maven"
    }

    stages {
        stage ('Git Fetch Stage') {
            steps{
                echo "Git Stage"
                git 'https://github.com/Aman10Siemens/Maven-Jenkins-Pipeline.git'
            }
        }
        stage ('Compile Stage') {
            steps{
			    echo "Compile Stage"
			    sh "mvn clean compile"
			 //   withMaven( maven : 'Java_Maven'){
			 //       sh "mvn clean compile"
			 //   }
			 //   def MavenHome = tool name: 'Java_Maven', type: 'maven'
                // def MavenCommand = "${MavenHome}/bin/mvn"
                // sh "${MavenCommand} clean compile"
            }
        }
        stage ('Test Stage'){
	        parallel{
		        stage('Test Compile Stage'){
			        steps{
					    echo "Compile Stage in Paralle;"
					    sh 'mvn test-compile'
			        }
		        }
		        stage('Test Cases Stage'){
			        steps{
						echo "Test Case Stage in Parallel"
					    sh 'mvn test'
			        }
		        }
	        }
        }
        stage ('Build Stage'){
            steps{
				echo "Build Stage"
                sh 'mvn install'
            }
        }
        stage ('SonarQube Analysis Stage'){
            steps{
				echo "SonarQube Stage"
            }
        }
    }
}
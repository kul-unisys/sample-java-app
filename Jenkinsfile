pipeline {
    // Added option to run build on specific agent
	agent {
		label ('kul')
	}
    
    // Adding Environemtn Section define Build Specific Environment Variables
    environment {
        JAVA_HOME = "/etc/alternatives/java_sdk_openjdk"
    }

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mvn_3.6.3"
    }

    stages {
        // Adding Sonar Analysis Stage for Static Scanning of Code for Potential Coe Quality issues
	stage('Sonar Analysis'){
	  steps {
	    git credentialsId: 'github-cred', url: 'https://github.com/kul-unisys/sample-java-app.git'
            sh "mvn -Dmaven.test.failure.ignore=true clean package sonar:sonar"
	  }
	}
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                //git 'https://github.com/kul-unisys/sample-java-app.git'
                git credentialsId: 'github-cred', url: 'https://github.com/kul-unisys/sample-java-app.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
		
		stage('OWASP DC Scan'){
			steps{
				sh "mvn clean install"
			}
		}
    }
}

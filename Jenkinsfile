pipeline {
	agent any 
	
	parameters {
		choice(name: 'ENV', choices: ['QA','UAT'], description: 'Pick Environment value')
	}	
	stages {
	    stage('Checkout') {
	        steps {
			checkout scm			       
		      }}
		stage('Build') {
	           steps {
			  sh '/home/piyush/Extracted/Maven_setup/apache-maven-3.9.6/bin/mvn install'
	                 }}
		stage('Deployment'){
		    steps {
			script {
			 if ( env.ENV == 'QA' ){
        	sh 'cp target/HOTSTAR.war /home/piyush/Extracted/apache-tomcat-9.0.88/webapps'
        	echo "deployment has been COMPLETED on QA!"
			 }
			else if ( env.ENV == 'UAT' ){
    		sh 'cp target/HOTSTAR.war /home/piyush/Extracted/apache-tomcat-9.0.88/webapps'
    		echo "deployment has been done on UAT!"
			}}}}
		stage( 'Slack' ) {
		    steps {
			slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#devops-slack', color: 'Good', message: 'welcome to jenkins', notifyCommitters: true, teamDomain: 'HOTSTAR', tokenCredentialId: '8e9fe88a-9e41-49a3-b318-76db094f5cc0'
}}	
}}

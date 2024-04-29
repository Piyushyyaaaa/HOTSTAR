pipeline {
	agent any 
	
	parameters {
  		string defaultValue: 'QA', name: 'ENV'
	}
	
	triggers {
  		pollSCM '* * * * *'
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
			else ( env.ENV == 'UAT' ){
    		sh 'cp target/HOTSTAR.war /home/piyush/Extracted/apache-tomcat-9.0.88/webapps'
    		echo "deployment has been done on UAT!"
slackSend channel: 'devops-slack', color: 'good', message: 'welcome to jenkins', teamDomain: 'devops', tokenCredentialId: '8e9fe88a-9e41-49a3-b318-76db094f5cc0'
			}
			}}}	
}}

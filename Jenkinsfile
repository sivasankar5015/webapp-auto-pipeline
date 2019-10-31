pipeline {

   agent any
   
    stages {
	
	   stage('Build') {
	       steps {
		       bat label: '', script: 'mvn clean package'
		   }
		   post {
		       success {
			         echo 'archiving the artifacts'
					 archiveArtifacts '**/*.war'
			   }
			   failure {
			         echo 'failed to archive'
			   }
		   
		   }
	   }
	   stage('checking the code quality') {
	       steps {
		       bat label: '', script: 'mvn checkstyle:checkstyle'
			   checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
		   }
	   
	   }
	   stage('deploy to staging') {
	       steps {
		       deploy adapters: [tomcat8(credentialsId: '694ccb90-0113-4b44-8dc5-bc4638ee2502', path: '', url: 'http://localhost:8211/manager/html')], contextPath: null, war: '**/*.war'
		   }
		   post {
		      success {
			        echo 'deployment is successful'
			  }
			  failure {
			        echo 'deployment is failed' 
			  }
		   }
	   
	   }
	   stage('deploy to production') {
	       steps {
		       deploy adapters: [tomcat8(credentialsId: 'c78cf8a3-7221-4013-8b84-cdfbf9d23d7f', path: '', url: 'http://localhost:8555/manager/html')], contextPath: null, war: '**/*.war'
		   }
		   post {
		      success {
			        echo 'deployment to production is successful'
			  }
			  failure {
			        echo 'failed to deploy'
			  }
		   }
	   
	   }
	
	
	
	}




}
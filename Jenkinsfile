pipeline {
 
 agent any
 
 stages {
    stage('build') {
	  steps {
	     bat label: '', script: 'mvn clean package'
	  }
	}
	stage('copy atrifacts') {
	  steps {
	    copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'job1', selector: lastSuccessful()
	  }
	}
	stage('deploy to tomcat') {
	  steps {
	    deploy adapters: [tomcat8(credentialsId: '694ccb90-0113-4b44-8dc5-bc4638ee2502', path: '', url: 'http://localhost:8222/manager/html')], contextPath: null, war: '**/*.war'
	  }
	}
	  
 }
}

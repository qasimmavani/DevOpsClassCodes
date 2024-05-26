
pipeline {
    agent any
    tools{
	jdk 'myjava'
	maven 'mymaven'    
    }	
    stages {
        stage('compile') {
	       steps {
              echo 'compiling..'
              git url: 'https://github.com/lerndevops/DevOpsClassCodes'
		          sh 'mvn compile'
           }
        }
        stage('codereview-pmd') {
	       steps {
                echo 'codereview..'
		            sh script: '/opt/apache-maven-3.6.3/bin/mvn -P metrics pmd:pmd'
           }
	        post {
               success {
		          recordIssues enabledForFailure: true, tool: pmdParser(pattern: '**/target/pmd.xml')
               }
           }		
        }
        stage('unit-test') {
	        steps {
                echo 'unittest..'
	             sh script: '/opt/apache-maven-3.6.3/bin/mvn test'
                 }
	        		
        }
        stage('codecoverate') {
	      steps {
                echo 'codecoverage..'
		         sh script: '/opt/apache-maven-3.6.3/bin/mvn cobertura:cobertura -Dcobertura.report.format=xml'
           }
	     		
        }
        stage('package') {
	      steps {
                echo 'package..'
		            sh script: '/opt/apache-maven-3.6.3/bin/mvn package'	
           }		
        }
    }
}

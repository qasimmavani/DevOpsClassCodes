
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
		            sh 'mvn -P metrics pmd:pmd'
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
	             sh 'mvn test'
                 }
	        		
        }
        stage('codecoverate') {
	      steps {
                echo 'codecoverage..'
		         sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
           }
	     		
        }
        stage('package') {
	      steps {
                echo 'package..'
		            sh 'mvn package'	
           }		
        }
    }
}

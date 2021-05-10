pipeline {
  agent any
	environment {
	  PATH = '/home/jenkins/.local/bin:/home/jenkins/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/jenkins/apache-maven-3.8.1/bin:/home/jenkins/apache-ant-1.10.10/bin'
	}

  stages {
    stage('Compile') {
       steps {
	        sh "mvn compile"
       }
    }

    stage('Build') {
	     steps {
          sh "mvn package"
	     }
    }

    stage('Install') {
	     steps {
          sh 'mvn install'
	     }
    }

    stage('Archieve') {
        steps {
           archiveArtifacts 'target/*.jar'
        }
    }

    stage('FingerPrint') {
        steps {
           fingerprint 'target/*.jar'
        }
    }

    stage('HTML_Publish') {
	     steps {
	         junit 'target/surefire-reports/TEST-*.xml'
        }
    }

    stage ('Email') {
             steps {
                 emailext body: 'Build is completed', replyTo: 'ketu1009@gmail.com', subject: 'Build is completed', to: 'ketu1009@gmail.com'
        }
    }

  }

}

pipeline {
  agent any

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

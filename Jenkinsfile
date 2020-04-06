def mvn
pipeline {
  agent { label 'master' }
    tools {
      maven 'Maven'
      jdk 'JAVA_HOME'
    }
  stages {
   stage ('Maven Build') {
      steps {
        script {
          mvn= tool (name: 'Maven', type: 'maven') + '/bin/mvn'
        }
        sh "${mvn} clean install"
      }
    }
  stage('Build Docker Image'){
    steps{
      sh 'docker build -t bhakya/sample-hello:$BUILD_NUMBER .'
    }
  }
  stage('Docker Container'){
    steps{
      sh 'docker login -u bhakya -p Login@1234'
      sh 'docker push bhakya/sample-hello:$BUILD_NUMBER'
	  sh 'docker run -d -p 8000:8000 --name SpringbootApp bhakya/sample-hello:$BUILD_NUMBER'
    
    }
  }  

  }
}

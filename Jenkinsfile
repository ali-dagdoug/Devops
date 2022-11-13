pipeline {
  agent any
  
  stages {

   stage('Checkout GIT ') {
            steps {
                echo 'Pulling ...';
                git branch: 'ali_dagdoug', url: 'https://github.com/ali-dagdoug/Devops.git'            }

        }
    stage('Testing maven'){
      steps {
        sh "mvn -version"
      }
	  }
    stage('MVN SONARQUBE'){
      steps {
       sh "mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=esprit"
      }
	  }
    stage('Build Maven Spring'){
                                                  steps{
                                                     sh "mvn  clean install"
                                                  }
                                              }
    
    }
}

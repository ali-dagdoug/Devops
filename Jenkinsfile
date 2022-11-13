pipeline {
  agent any
  
  stages {

   stage('Checkout GIT ') {
            steps {
                echo 'Pulliing ...';
                git branch: 'ali_dagdoug', url: 'https://github.com/ali-dagdoug/Devops.git'            }

        }
    stage('Testing maven'){
      steps {
        sh "mvn -version"
      }
	stage('Cleaning') {
                                      steps {
                                       script {
                                        echo 'cleaning';
                                        sh 'mvn clean '
                                       }
                                      }
                                    }
    
    }
  }
}

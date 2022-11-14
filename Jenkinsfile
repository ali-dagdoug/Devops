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
    stage('COMPILING') { steps { sh 'mvn compile' } }
            stage('MVN CLEAN') {
            steps {
                sh 'mvn clean';
            }
        }
        stage('MVN INSTALL') {
            steps {
                sh 'mvn install -DskipTests'
            }
        }
      stage('MVN SONARQUBE'){
      steps {
       sh "mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=esprit"
      }
	  }
    
    stage('NEXUS')
      {
      steps{
      echo "nexus"
      sh "mvn clean deploy -DskipTests"
            }
        }
       stage('Build docker image'){
                             steps{
                                 script{
                                    sh 'docker build -t alidagdoug/examen .'
                                 }
                             }
                         }

		stage("Maven Build") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
            }
        }

		 		 stage('Docker login') {

                                         steps {
                                          sh 'echo "login Docker ...."'
                   	sh 'docker login -u alidagdoug -p AM20407382dg'
                               }  }
		 stage('Docker push') {

                 steps {
                      sh 'echo "Docker is pushing ...."'
                     	sh 'docker push alidagdoug/examen'
                        }  }
        stage('DOCKER COMPOSE') {
            steps{
                sh "docker-compose up -d"
            }
        }
    
    }
}

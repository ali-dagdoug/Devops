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
    stage('Build Maven Spring'){
          steps{
            sh "mvn  clean install"
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
        stage('BUILD IMAGE') {
            steps {
                script {
                    dockerImage = docker.build registry + ":latest"
                }
            }
        }
        stage('PUSH IMAGE') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('REMOVE UNUSED DOCKER IMAGE') {
            steps{
                sh "docker rmi $registry:latest"
            }
        }
        stage('DOCKER COMPOSE') {
            steps{
                sh "docker-compose up -d"
            }
        }
    
    }
}

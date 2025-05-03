pipeline {
    agent any
   
    stages {
        
        stage('Drop the Apache Tomcat Docker container'){
            steps {
            echo 'droping the container...'
            sh 'docker rm -f tomcat1'
            }
        }
        stage('Create the Tomcat container') {
            steps {
            echo 'Creating the container...'
            sh 'docker run -dit --name tomcat1 -p 9090:8080  -v /home/developer/tomcat-web:/usr/local/tomcat/webapps tomcat:9.0'
            }
        }
    }

    post {

        always{
            echo 'Esto siempre se ejecuta independiente si es exitoso o no el pipeline'
            
        }
        success {
        // One or more steps need to be included within each condition's block.
        echo 'the deployment has worked'
        archiveArtifacts allowEmptyArchive: true, artifacts: 'shopping/*.jsp', followSymlinks: false
        cleanWs() //Elimina el workspace al terminar el pipeline

       }
       failure {
        // One or more steps need to be included within each condition's block.
        echo 'An error has ocurred'
      }
 }
}

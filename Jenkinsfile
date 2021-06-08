// Pipeline declarativo
pipeline{
    // Ejecutar en cualquier nodo
  agent {
    node {
      label 'principal'
    }
  }
  options{
    //Ficheros de Log
    buildDiscarder logRotator (
      daysToKeepStr: '15',
      numToKeepStr: '10'
    )
  }
    
    //Opciones pipeline
    options {
        
        //Detener ejecucion si tarda mas de 8min (generando fallo)
        timeout(time: 8)
        
    }
    
    // Programar disparador
    triggers{
        //Ejecutar cada minuto
        cron('* * * * *')
    }
    //Array de parametros
    parameters{
    
        booleanParam(name: 'TEST', defaultValue: true, description: '¿Es un BUILD para Testing?')
    }
    //FAses
    stages{
        stage('Cleanup Workspace'){
            //Crear variable de entorno
        
            steps{
              cleanWs()
              echo "Eliminado Workspace para Job";
 
             }
         }
         stage('Code Checkout') {
            
            steps {
                checkout(
                  $class: 'GitSCM',
                  branches: [[name: '*/main']],
                  userRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']]
                )
            }
     
        }
         stage('Unit Testing'){
            steps{
              echo "Running Units Test";
 
         }
         stage('Code Analisis'){
            steps{
              echo "Running Code Analisis";
          }
          stage('Build Deploy Code'){
            steps{
              echo "Running Building Artifact";
              echo "Deploying Code;"
          }
      }
   }

        
    

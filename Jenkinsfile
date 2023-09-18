
pipeline {
   agent any
   tools{
       jdk 'JDK1.8'
       maven 'Maven3.3.3'
   }
   options {
       timestamps()
       buildDiscarder(logRotator(artifactDaysToKeepStr: '10', artifactNumToKeepStr: '10', daysToKeepStr: '10', numToKeepStr: '10'))
   }
 stages {
     stage ('Display PATH of Jenkins'){
         steps {
             sh '''
             echo "This is Declarative pipeline for building ServiceApp"
             echo "PATH = ${PATH}"
             '''
         }
     }
     stage ('Checkout the Source Code') {
        steps {
         checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '3fc2aada-06ec-4327-abcc-3334d4595966', url: 'https://github.com/ravir1981/serviceApp.git']]])
        }
    }
      stage ('Building the Souce using Maven') {
          steps {
              sh 'mvn clean compile install'
          }
      }
      stage ('Archive artifacts for ServiceApp'){
          steps{
              archiveArtifacts '**/**/*.war'
          }
      }
    stage ('Create Docker image for ServiceApp'){
          steps{
              sh 'docker build -t serviceapp -f sm-shop/Dockerfile .'
          }
      }
    }
}

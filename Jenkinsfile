pipeline {
  agent any
    
triggers{
pollSCM('* * * * *')
}
options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
}
  stages {
        
    stage('Git') {
      steps {
        git branch: 'master', credentialsId: '984d5de4-a336-4d3c-ba3f-ba6fad40e902', url: 'https://github.com/RanjithaRajkumar/the-example-app.nodejs.git'
      }
    }
  // stage('DeployAppIntoNode'){
  //   steps{
  //    sshagent(['node-server']) {
  //      sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/NodeJS_Sample_app_pipeline ubuntu@34.222.48.98:/home/ubuntu/the-example-app.nodejs/"    
  // }
  // }
  // }
  stage ('Deploy') {
    steps{
        sshagent(credentials : ['node-server']) {
            sh "ssh -o StrictHostKeyChecking=no ubuntu@34.222.48.98 'echo /var/lib/jenkins'"
            sh 'ssh -v ubuntu@34.222.48.98'
            sh 'scp /var/lib/jenkins/workspace/NodeJS_Sample_app_pipeline_master/ ubuntu@34.222.48.98:/home/ubuntu/the-example-app.nodejs/'
        }
    }
}                                                                                                                                          
    stage('Build') {
      steps {
        sh 'ssh ubuntu@34.222.48.98 npm install && npm run start:master'
      }
    }  
  }

}
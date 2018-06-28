// some comment8

def createBooleanParameter(String desc, String value){

   return [$class: 'BooleanParameterDefinition', defaultValue: true, description: desc, name: value]

}



node (label: 'slave') {
  
def userInput = input(

 id: 'userInput', message: 'The below Scenarios failed, let\'s rerun them?', parameters: [

    createBooleanParameter('ScenarioA','Platform1-VariantA'),

    createBooleanParameter('ScenarioB','Platform1-VariantB'),

    createBooleanParameter('ScenarioC','Platform3-VariantA')

 ])

 
 // BooleanParameters are based on Key=> String based and Value=> Boolean based
 // then iterate through the list of parameters which are enable

 userInput?.findAll{ it.value }?.each {

    println it.key.toString()
 }    
    
//properties([parameters([choice(choices: ['TESTING', 'STAGING', 'PRODUCTION'], description: 'The target environment', name: 'DEPLOY_ENV')])])
   
  
//stage ('echo') {
//    echo "Will deploy to ${DEPLOY_ENV}"
//}

    
//def mvnHome = tool 'Maven 3.5.4'
// Maven 3.5.4    
stage('Clean workspace before build') {
    step([$class: 'WsCleanup'])
 }
stage('git') {
    git branch: 'master', url: 'https://github.com/Mikola3/simple-java-maven-app.git'
}
stage('pollSCM') {
    properties([pipelineTriggers([pollSCM('* * * * *')])])
}    
stage('Build') {
     sh '/opt/maven/bin/mvn -f pom.xml clean install'
     //sh '/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/Maven_3.5.4/bin/mvn -f pom.xml clean install'
}
stage ('Run') {
    sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
}
stage ('Unarchive & Archive') {
    sh 'tar -czf ${WORKSPACE}/pipeline-${BUILD_NUMBER}.tar.gz target/my-app-1.0-SNAPSHOT.jar'
}
}

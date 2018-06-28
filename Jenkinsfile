// some comment7
node (label: 'slave') {
//properties([parameters([choice(choices: ['TESTING', 'STAGING', 'PRODUCTION'], description: 'The target environment', name: 'DEPLOY_ENV')])])
defaultChoices = ["TESTING", "STAGING", "PRODUCTION"]
choices = createChoicesWithPreviousChoice(defaultChoices, "${params.CHOICE}")

properties([
    parameters([
        choice(name: "CHOICE", choices: choices.join("\n"))
    ])   
])
    
    
//stage ('echo') {
//    echo "Will deploy to ${DEPLOY_ENV}"
//}

stage ('echo') {
    echo "Will deploy to ${params.CHOICE}"
}    

List createChoicesWithPreviousChoice(List defaultChoices, String previousChoice) {
    if (previousChoice == null) {
       return defaultChoices
    }
    choices = defaultChoices.minus(previousChoice)
    choices.add(0, previousChoice)
    return choices
}    
    
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

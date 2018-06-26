// some comment2
node {
parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
stage ('Greet') {
    sh 'echo "${params.Greeting} World!"'
}    
def mvnHome = tool 'Maven 3.5.4'
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
     //sh '/opt/maven/bin/mvn -f pom.xml clean install'
     sh '/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/Maven_3.5.4/bin/mvn -f pom.xml clean install'
}
stage ('Run') {
    sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
}
stage ('Unarchive & Archive') {
    sh 'tar -czf ${WORKSPACE}/pipeline-${BUILD_NUMBER}.tar.gz target/my-app-1.0-SNAPSHOT.jar'
}

}

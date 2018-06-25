// comment
node {
stage('Clean workspace before build') {
    step([$class: 'WsCleanup'])
 }
stage('git') {
    git branch: 'master', url: 'https://github.com/Mikola3/simple-java-maven-app.git'
 }
stage('Build') {
     maven: 'Maven 3.5.4',
     mvn -f pom.xml clean install'
     // sh '/opt/maven/bin/mvn -f pom.xml clean install'
}
stage ('Run') {
    sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
}
 
}

// comment
node {
stage('Clean workspace before build') {
    step([$class: 'WsCleanup'])
 }
stage('git') {
    git branch: 'master', url: 'https://github.com/Mikola3/simple-java-maven-app.git'
 }
stage('Build') {
     // sh '/opt/maven/bin/mvn -f pom.xml clean install'
     mvn -f pom.xml clean install'
}
stage ('Run') {
    sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
}
 
}

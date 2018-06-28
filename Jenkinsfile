// some comment8
node (label: 'slave') {
    
//properties([parameters([choice(choices: ['TESTING', 'STAGING', 'PRODUCTION'], description: 'The target environment', name: 'DEPLOY_ENV')])])
   
  
//stage ('echo') {
//    echo "Will deploy to ${DEPLOY_ENV}"
//}

    
pipeline {
    agent any
    stages {
        stage("robot test") {
            steps {
                script {
                    MYLIST = []
                    MYLIST += "param-one"
                    MYLIST += "param-two"
                    MYLIST += "param-three"
                    MYLIST += "param-four"
                    MYLIST += "param-five"

                    for (def element = 0; element < MYLIST.size(); element++) {
                        build(
                            job: 'parameterized-job',
                            parameters: [
                                [
                                    $class: 'StringParameterValue',
                                    name: 'MYLIST',
                                    value: MYLIST[element]
                                ]
                            ]
                        )
                    }
                }
            }
        }
    }
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

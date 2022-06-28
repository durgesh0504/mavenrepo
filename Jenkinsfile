pipeline{
agent {label 'devslave1'}

triggers {
        pollSCM '* * * * *'
    }

stages{

stage('scm'){
steps{
checkout([$class: 'GitSCM', branches: [[name: '*/feat01']], extensions: [], userRemoteConfigs: [[credentialsId: 'ac4e63e8-736e-4f38-9cba-4303ed46bbd3', url: 'https://github.com/durgesh0504/mavenrepo.git']]])
}
}

stage('build'){
steps{
sh 'mvn package'
}
}

stage('sonar'){
steps{
withSonarQubeEnv('sonarqube999') {
    sh 'mvn sonar:sonar'
}
}
}

stage('nexus'){
steps{
sh 'mvn deploy'
}
}

stage('tomcat'){
steps{
sh 'scp /root/workspace/durgesh/target/studentapp-2.1.1-FEAT01-SNAPSHOT.war root@13.126.25.11:/var/lib/tomcat/webapps' 
}
}

}
}


pipeline{
agent { label 'devserver1' }
stages{
stage('1'){
steps{
checkout([$class: 'GitSCM', 
    branches: [[name: '*/master']], 
    userRemoteConfigs: [[credentialsId: 'c842b84c-2283-48eb-8ea1-495da8464f7c', url: 'https://github.com/derangula/mavenrepo.git']]
])

}
}
stage('build'){
steps{
sh 'mvn package'

}
}

stage('sonar'){
steps{
withSonarQubeEnv('sonar'){
sh "mvn sonar:sonar"
}


}
}

stage('tomcat'){
steps{
sh 'scp /root/workspace/samplejob/target/studentapp-2.5-SNAPSHOT.war 3.21.207.196:/var/lib/tomcat/webapps'

}
}

}
}

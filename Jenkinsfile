node {
    
    def mavenHome = tool name: "maven3.8.4"
    
    stage('Preparation') { 
    git branch: 'development', credentialsId: '5657b417-b021-4b33-82b9-a5416d6e9f01', url:
    'https://github.com/vijiptl/maven-web-application.git'
    }
    
    stage('Build') {
        sh "${mavenHome}/bin/mvn clean package"
    }
    
    stage('Sonar to Sonar'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
    stage('Nexus underControl'){
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    
    stage('Tom to Cat'){
        sshagent(['fc25114a-735e-49ba-b2ad-c5b276eb381a']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@ec2-13-232-28-175.ap-south-1.compute.amazonaws.com:/opt/Tomcat9/webapps"
}
    }

}

node
{
    def mavenHome = tool name: "maven3.8.4"
    
    stage('CheckoutCode')
    {
        git branch: 'development', credentialsId: '0a822100-ecfa-4bcd-a7e0-bc5a4808d23f', url:
        'https://github.com/vijiptl/maven-web-application.git'
    }
    
    stage('Buildpackage'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    
    stage('SonarRun'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}

stage('NexusArtifact'){
    sh "${mavenHome}/bin/mvn clean deploy"
}

stage ('Tomcatdeploy'){
    sshagent(['7270cea8-9195-4507-8750-2f92077e6963']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.95.39:/opt/tomcat9/webapps/"
}
  }

stage('EmailNotification'){
emailext body: 'Build Report', subject: 'Build Report', to: 'vijayptlp@gmail.com'
    
}
}

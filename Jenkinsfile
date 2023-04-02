pipeline{
    agent any;
    stages{
        stage('Pulling code'){
            steps{
                git credentialsId: 'Git_credential', url: 'https://github.com/ANILPHUGARE1/maven-web-application.git'
            }
        }
        stage('Build code'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Upload War Nexus'){
            steps{
                nexusPublisher nexusInstanceId: 'Maven_Repository', nexusRepositoryId: 'Maven_Repository', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/lib/jenkins/workspaces/Maven_application_upload_on-Nexus/target/**/*.war']], mavenCoordinate: [artifactId: 'maven-web-application', groupId: 'com.mt', packaging: 'war', version: '0.0.1-SNAPSHOT']]]
            }
        }
        stage('Deploy'){
            steps{
                deploy adapters: [tomcat7(credentialsId: 'Tomcat_credential', path: '', url: 'http://3.111.245.195:8080/')], contextPath: 'maven-web-application', war: '**/*.war'
            }
        }
    }
}

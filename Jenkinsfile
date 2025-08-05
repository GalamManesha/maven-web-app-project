pipeline {
    agent any
    tools{
	maven "maven3.9.9"
	}
    stages {
        stage("gitcheclout") {
            steps {
               git 'https://github.com/GalamManesha/maven-web-app-project.git'
            }
        }
        stage('compile'){
    steps{
     sh "mvn compile"
	}
}
stage('sonar')
{
    steps{
        sh "mvn clean sonar:sonar"
    }
}
stage ("nexus report"){
steps{
    sh "mvn deploy"
}
}
stage('Deploy to Tomcat') {
            steps {
                sh """
                    curl -u manesha:password \\
                    --upload-file /var/lib/jenkins/workspace/declarative-way/target/maven-web-application.war \\
                    "http://47.129.45.5:8080/manager/text/deploy?path=/maven-web-application&update=true"
                """
            }
        }
    }
}

node
{

   echo "git branch name: ${env.BRANCH_NAME}"
   echo "build number is: ${env.BUILD_NUMBER}"
   echo "node name is: ${env.NODE_NAME}"


   // /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven3.9.9/bin
   def mavenHome=tool name: "maven3.9.9"
    try
    {

  stage('git checkout')
  {
    notifyBuild('STARTED')
    git branch: 'master', url: 'https://github.com/kkdevopsb5/maven-webapplication-project-kkfunda.git'
  } 

    stage('COMPILE')
  {
    sh "${mavenHome}/bin/mvn clean compile"
  }

  stage('Build')
  {
    sh "${mavenHome}/bin/mvn clean package"
  }

    stage('SQ Report')
  {
    sh "${mavenHome}/bin/mvn sonar:sonar"
  }

      stage('Upload Artifact')
  {

    sh "${mavenHome}/bin/mvn clean deploy"
  }

    stage('Deploy to Tomcat') 
    {
      
      sh """

      curl -u manesha:password \
--upload-file /var/lib/jenkins/workspace/MBPL-First/target/maven-web-application.war \
"http://47.129.45.5:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
    }
    }

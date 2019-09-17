node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      sh '''
         java -version
         cd initial
         mvn clean package
         cd target
         cp ../src/main/resources/web.config web.config
         cp gs-spring-boot-0.1.0.jar app.jar 
         zip springboot.zip app.jar web.config
      '''
   }
   stage('deploy') {
       sh '''
         pwd
      '''
      azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID,
      resourceGroup: env.RES_GROUP, appName: env.WEB_APP, filePath: "**/springboot.zip"
   }
}

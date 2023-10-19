import groovy.json.JsonSlurper

def getAcrLoginServer(def acrSettingsJson) {
  def acrSettings = new JsonSlurper().parseText(acrSettingsJson)
  return acrSettings.loginServer
}

node {
  stage('init') {
    checkout scm
  }
  
  stage('build') {
    sh 'mvn clean package'
  }

  stage('Dockerize-admin-server') {
    withCredentials([azureServicePrincipal('azure-credentials')]) {
      def acrName = 'kpnreg'
      def imageName = 'spring-petclinic-admin-server'
      // get login server
      def acrSettingsJson = sh script: "az acr show -n $acrName", returnStdout: true
      def loginServer = getAcrLoginServer acrSettingsJson
      sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
      
      // build image
      def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
      sh "cd $imageName && docker build -t $imageWithTag ."
      sh "docker push $imageWithTag"
      sh "docker logout $loginServer"
    }
  }

  stage('Dockerize-api-gateway') {
    withCredentials([azureServicePrincipal('azure-credentials')]) {
      def acrName = 'kpnreg'
      def imageName = 'spring-petclinic-api-gateway'
      // get login server
      def acrSettingsJson = sh script: "az acr show -n $acrName", returnStdout: true
      def loginServer = getAcrLoginServer acrSettingsJson
      sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
      
      // build image
      def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
      sh "cd $imageName && docker build -t $imageWithTag ."
      sh "docker push $imageWithTag"
      sh "docker logout $loginServer"
    }
  }

  stage('Dockerize-config-server') {
    withCredentials([azureServicePrincipal('azure-credentials')]) {
      def acrName = 'kpnreg'
      def imageName = 'spring-petclinic-config-server'
      // get login server
      def acrSettingsJson = sh script: "az acr show -n $acrName", returnStdout: true
      def loginServer = getAcrLoginServer acrSettingsJson
      sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
      
      // build image
      def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
      sh "cd $imageName && docker build -t $imageWithTag ."
      sh "docker push $imageWithTag"
      sh "docker logout $loginServer"
    }
  }

  stage('Dockerize-customers-service') {
    withCredentials([azureServicePrincipal('azure-credentials')]) {
      def acrName = 'kpnreg'
      def imageName = 'spring-petclinic-customers-service'
      // get login server
      def acrSettingsJson = sh script: "az acr show -n $acrName", returnStdout: true
      def loginServer = getAcrLoginServer acrSettingsJson
      sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
      
      // build image
      def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
      sh "cd $imageName && docker build -t $imageWithTag ."
      sh "docker push $imageWithTag"
      sh "docker logout $loginServer"
    }
  }

  stage('Dockerize-discovery-server') {
    withCredentials([azureServicePrincipal('azure-credentials')]) {
      def acrName = 'kpnreg'
      def imageName = 'spring-petclinic-discovery-server'
      // get login server
      def acrSettingsJson = sh script: "az acr show -n $acrName", returnStdout: true
      def loginServer = getAcrLoginServer acrSettingsJson
      sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
      
      // build image
      def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
      sh "cd $imageName && docker build -t $imageWithTag ."
      sh "docker push $imageWithTag"
      sh "docker logout $loginServer"
    }
  }

  stage('Dockerize-vets-service') {
    withCredentials([azureServicePrincipal('azure-credentials')]) {
      def acrName = 'kpnreg'
      def imageName = 'spring-petclinic-vets-service'
      // get login server
      def acrSettingsJson = sh script: "az acr show -n $acrName", returnStdout: true
      def loginServer = getAcrLoginServer acrSettingsJson
      sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
      
      // build image
      def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
      sh "cd $imageName && docker build -t $imageWithTag ."
      sh "docker push $imageWithTag"
      sh "docker logout $loginServer"
    }
  }

  stage('Dockerize-visits-service') {
    withCredentials([azureServicePrincipal('azure-credentials')]) {
      def acrName = 'kpnreg'
      def imageName = 'spring-petclinic-visits-service'
      // get login server
      def acrSettingsJson = sh script: "az acr show -n $acrName", returnStdout: true
      def loginServer = getAcrLoginServer acrSettingsJson
      sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
      
      // build image
      def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
      sh "cd $imageName && docker build -t $imageWithTag ."
      sh "docker push $imageWithTag"
      sh "docker logout $loginServer"
    }
  }
  
  stage('deploy') {
    
    // generate version, it's important to remove the trailing new line in git describe output
    withCredentials([azureServicePrincipal('azure-credentials')]) {
      // login Azure
      sh '''
        az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID
        az account set -s $AZURE_SUBSCRIPTION_ID
      '''
      
      
      // update deployment.yaml with latest tag
      sh "sed 's/\$version/$BUILD_NUMBER/g' k8s-manifests/deployment.yaml > target/deployment.yaml"
      // update deployment
      sh 'kubectl apply -f target/deployment.yaml'
      // log out
      sh 'az logout'
      
    }
  }
}

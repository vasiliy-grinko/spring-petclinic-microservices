pipeline {
  agent any
  stages {
    stage('init') {
      steps { 
          checkout scm
      }
    }

    stage('build') {
      steps { 
        sh 'mvn clean package'
      }
    }

    stage('Push to ACR: admin-server') {
      steps {
        script {
          withCredentials([azureServicePrincipal('azure-credentials')]) {
            def acrName = 'kpnreg'
            def imageName = 'spring-petclinic-admin-server'
            // get login server
            
            // def acrSettingsJson = sh script: "az acr show -n $acrName", returnStdout: true
            def loginServer = "kpnreg.azurecr.io"
            sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
            
            // Build and push image
            def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
            sh "echo $imageName"
            sh "docker build -t $imageWithTag -f $imageName/Dockerfile $imageName"
            sh "docker push $imageWithTag"
            sh "docker logout $loginServer"
            sh "export IMAGE_TAG=$imageWithTag"
            dir ('versioned-k8s-manifests') {}
            // sh(script: "yq -i '.spec.template.spec.containers[0].image = strenv(IMAGE_TAG)' k8s-manifests/${imageName}.yaml")
            sh (script: "sed \"s/version/$BUILD_NUMBER/g\" k8s-manifests/${imageName}.yaml > versioned-k8s-manifests/${imageName}.yaml")
            sh(script: "cat k8s-manifests/${imageName}.yaml")
          }
        }
      }
    }

    stage('Push to ACR: api-gateway') {
      steps {
        script {
          withCredentials([azureServicePrincipal('azure-credentials')]) {
            def acrName = 'kpnreg'
            def imageName = 'spring-petclinic-api-gateway'
            // get login server
            def loginServer = "kpnreg.azurecr.io"
            sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
            
            // Build and push image
            def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
            sh "echo $imageName"
            sh "docker build -t $imageWithTag -f $imageName/Dockerfile $imageName"
            sh "docker push $imageWithTag"
            sh "docker logout $loginServer"
            sh "export IMAGE_TAG=$imageWithTag"
            dir ('versioned-k8s-manifests') {}
            sh (script: "sed \"s/version/$BUILD_NUMBER/g\" k8s-manifests/${imageName}.yaml > versioned-k8s-manifests/${imageName}.yaml")
            sh(script: "cat k8s-manifests/${imageName}.yaml")
          }
        }
      }
    }

    stage('Push to ACR: config-server') {
      steps { 
        script {
          withCredentials([azureServicePrincipal('azure-credentials')]) {
            def acrName = 'kpnreg'
            def imageName = 'spring-petclinic-config-server'
            def loginServer = "kpnreg.azurecr.io"
            sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
            
            // Build and push image
            def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
            sh "echo $imageName"
            sh "docker build -t $imageWithTag -f $imageName/Dockerfile $imageName"
            sh "docker push $imageWithTag"
            sh "docker logout $loginServer"
            sh "export IMAGE_TAG=$imageWithTag"
            dir ('versioned-k8s-manifests') {}
            sh (script: "sed \"s/version/$BUILD_NUMBER/g\" k8s-manifests/${imageName}.yaml > versioned-k8s-manifests/${imageName}.yaml")
            sh(script: "cat k8s-manifests/${imageName}.yaml")
          }
        }
      }
    }

    stage('Push to ACR: customers-service') {
      steps { 
        script {
          withCredentials([azureServicePrincipal('azure-credentials')]) {
            def acrName = 'kpnreg'
            def imageName = 'spring-petclinic-customers-service'
            def loginServer = "kpnreg.azurecr.io"
            sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
            
            // Build and push image
            def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
            sh "echo $imageName"
            sh "docker build -t $imageWithTag -f $imageName/Dockerfile $imageName"
            sh "docker push $imageWithTag"
            sh "docker logout $loginServer"
            sh "export IMAGE_TAG=$imageWithTag"
            dir ('versioned-k8s-manifests') {}
            sh (script: "sed \"s/version/$BUILD_NUMBER/g\" k8s-manifests/${imageName}.yaml > versioned-k8s-manifests/${imageName}.yaml")
            sh(script: "cat k8s-manifests/${imageName}.yaml")
          }
        }
      }
    }

    stage('Push to ACR: discovery-server') {
      steps { 
        script {
          withCredentials([azureServicePrincipal('azure-credentials')]) {
            def acrName = 'kpnreg'
            def imageName = 'spring-petclinic-discovery-server'
            def loginServer = "kpnreg.azurecr.io"
            sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
            
            // Build and push image
            def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
            sh "echo $imageName"
            sh "docker build -t $imageWithTag -f $imageName/Dockerfile $imageName"
            sh "docker push $imageWithTag"
            sh "docker logout $loginServer"
            sh "export IMAGE_TAG=$imageWithTag"
            dir ('versioned-k8s-manifests') {}
            sh (script: "sed \"s/version/$BUILD_NUMBER/g\" k8s-manifests/${imageName}.yaml > versioned-k8s-manifests/${imageName}.yaml")
            sh(script: "cat k8s-manifests/${imageName}.yaml")
          }
        }
      }
    }

    stage('Push to ACR: vets-service') {
      steps { 
        script {
          withCredentials([azureServicePrincipal('azure-credentials')]) {
            def acrName = 'kpnreg'
            def imageName = 'spring-petclinic-vets-service'
            def loginServer = "kpnreg.azurecr.io"
            sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
            
            // Build and push image
            def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
            sh "echo $imageName"
            sh "docker build -t $imageWithTag -f $imageName/Dockerfile $imageName"
            sh "docker push $imageWithTag"
            sh "docker logout $loginServer"
            sh "export IMAGE_TAG=$imageWithTag"
            dir ('versioned-k8s-manifests') {}
            sh (script: "sed \"s/version/$BUILD_NUMBER/g\" k8s-manifests/${imageName}.yaml > versioned-k8s-manifests/${imageName}.yaml")
            sh(script: "cat k8s-manifests/${imageName}.yaml")
          }
        }
      }
    }

    stage('Push to ACR: visits-service') {
      steps { 
        script {
          withCredentials([azureServicePrincipal('azure-credentials')]) {
            def acrName = 'kpnreg'
            def imageName = 'spring-petclinic-visits-service'
            def loginServer = "kpnreg.azurecr.io"
            sh "docker login -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET $loginServer"
            
            // Build and push image
            def imageWithTag = "$loginServer/$imageName:$BUILD_NUMBER"
            sh "echo $imageName"
            sh "docker build -t $imageWithTag -f $imageName/Dockerfile $imageName"
            sh "docker push $imageWithTag"
            sh "docker logout $loginServer"
            sh "export IMAGE_TAG=$imageWithTag"
            dir ('versioned-k8s-manifests') {}
            sh (script: "sed \"s/version/$BUILD_NUMBER/g\" k8s-manifests/${imageName}.yaml > versioned-k8s-manifests/${imageName}.yaml")
            sh(script: "cat k8s-manifests/${imageName}.yaml")
          }
        }
      }
    }
    
    stage('Deploy to AKS') {
      steps { 
        script {
        // generate version, it's important to remove the trailing new line in git describe output
          withCredentials([azureServicePrincipal('azure-credentials')]) {
            // login Azure
            sh '''
              az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID
              az account set -s $AZURE_SUBSCRIPTION_ID
              az aks get-credentials -a --name cluster-awake-tadpole --resource-group kpn
            '''
            sh 'kubectl apply -f versioned-k8s-manifests'
            sh 'az logout'
          }
        }
      }
    }
  }
}

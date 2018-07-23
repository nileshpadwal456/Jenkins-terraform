pipeline {

  agent any

  stages {

    stage('TF Plan') {
      steps {
          sh 'terraform init'
          sh 'terraform plan -var env=${env} -out myplan'
      }
    }

    stage('Approval') {
      steps {
        script {
          def userInput = input(id: 'confirm', message: 'Apply Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
        }
      }
    }

    stage('TF Apply') {
      steps {
          sh 'terraform apply -input=false myplan'
      }
    }

  }

}

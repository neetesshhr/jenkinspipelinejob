node{
    
   

    
       properties([
        parameters([
            string(name: 'IMAGE_NAME', defaultValue: 'python-app', description: 'The name of the image to build'),
            string(name: 'IMAGE_TAG', defaultValue: 'latest', description: 'The tag of the image to build'),
            choice(name: 'ENVIRONMENT', defaultValue: 'dev', description: 'The type of ENVIRONMENT to perform build', choices: ['dev', 'prod', 'uat']),
            // boolean(name: 'isWorking', defaultValue: true, description: 'Is this Working'),
            string(name: 'REQ_INC', defaultValue: 'SQX', description: 'The REQ_INC')
        ])
       ])
        stage('Set build name'){
            checkout scm
        currentBuild.description = "${params.REQ_INC}"
        currentBuild.displayName = "${params.REQ_INC}"
        currentBuild.buildName
    }

    
   
    stage('Build image'){
        echo 'Building image...'
        bat '''docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'''
    }
    post{
        always{
            emailext body: 'A test email from Jenkins', recipientProviders: [[$class: 'DeveloperRecipientProvider'], 
            [$class: 'RequestRecipientProvider']], subject: 'Test email from Jenkins'
        }
    }
}
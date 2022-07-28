node{
        properties([
        parameters([
            string(name: 'IMAGE_NAME', defaultValue: 'python-app', description: 'The name of the image to build'),
            string(name: 'IMAGE_TAG', defaultValue: 'latest', description: 'The tag of the image to build'),
            choice(name: 'ENVIRONMENT', defaultValue: 'dev', description: 'The type of ENVIRONMENT to perform build', choices: ['dev', 'prod', 'uat']),
            // boolean(name: 'isWorking', defaultValue: true, description: 'Is this Working'),
          
        ])
       ])
     try { 
        notifyBuild("STARTED")   
        stage('Set build name'){
            checkout scm
       }

    
   
    stage('Build image'){
        echo 'Building image...'
        bat '''docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'''
    }
     }catch (e) {
        currentBuild.result = "FAILED"
        throw e
     } finally {
        notifyBuild(currentBuild.result)
  }
}
 
 def notifyBuild(String buildStatus  = 'STARTED')  {
    buildStatus = buildStatus ?: 'SUCCESS'

    def colorName = 'RED'
    def colorCode = '#FF0000'
    def subject = "${buildStatus}: Job '${env.JOB_NAME}' [${env.BUILD_NUMBER}]"
    def summary = "${subject} (${env.BUILD_URL})"
    def details = """<p> STARTED JOB '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
    <p> Check console output at &QUOT; <a href='${env.BUILD_URL}'${env.JOB_NAME}[${env.BUILD_NUMBER}]</a> &QUOT;</p>"""


    if (buildStatus == 'STARTED') {
        color = 'YELLOW'
        colorCode = '#FFFF00'
    }else if(buildStatus == 'SUCCESS') {
        color = 'GREEN'
        colorCode = '#00FF00'
    }else{
        color = 'RED'
        colorCode = '#FF0000'
    }

    emailext (
        subject: subject,
        body: details,
        recipientProviders: [[$class: 'DevelopersRecipientProvider']],
    )
 }

node{
        properties([
        parameters([
            string(name: 'IMAGE_NAME', defaultValue: 'python-app', description: 'The name of the image to build'),
            string(name: 'IMAGE_TAG', defaultValue: 'latest', description: 'The tag of the image to build'),
            choice(name: 'ENVIRONMENT', defaultValue: 'dev', description: 'The type of ENVIRONMENT to perform build', choices: ['dev', 'prod', 'uat']),
            // boolean(name: 'isWorking', defaultValue: true, description: 'Is this Working'),
          
        ])
       ])
        echo "${IMAGE_NAME}"
}

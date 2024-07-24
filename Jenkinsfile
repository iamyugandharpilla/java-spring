pipeline { 
   agent any

    stages {
        stage ('build') {
            steps {
                sh '''cd $WORKSPACE
                      docker build -t java-spring-19.1:v${BUILD_NUMBER} . '''
            }
        }
        stage('image push ECR') {
            steps {
                sh '''aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 767397709049.dkr.ecr.us-east-1.amazonaws.com

                                         docker tag java-spring-19.1.${BUILD_NUMBER} 767397709049.dkr.ecr.us-east-1.amazonaws.com/java-spring-19.1.${BUILD_NUMBER}
                         docker push 767397709049.dkr.ecr.us-east-1.amazonaws.com/java-spring-19.1.${BUILD_NUMBER}

        '''
            }
          }

} 
    post{
        always{
            emailext body: '''Hi,

     The jenkins has been failed . please check it.

     Thanks
     Devops Team''', subject: 'testing jenkins pipeline: $JOB_URL', to: 'yugandharpilla@outlook.com'
    }
    }
}

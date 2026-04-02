pipeline {
  agent any
  environment {
    APP_NAME = "spring-petclinic"
    DEV_TEAM = 'akshathabm20@gmail.com'
    BUILD_INFO = "Job_Name: ${env.JOB_NAME}\nBuild_Number: ${env.BUILD_NUMBER}"
  }
  tools {
    jdk "java-home"
    maven "maven-home"
  }
  stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Akshathabm786/Fork-spring-petclinic.git'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
              archiveArtifacts artifacts:'target/*.jar', fingerprint:true
            }
        }
  }
  post {
        success {
            mail to: 'akshathabm20@gmail.com',
                cc: "${env.DEV_TEAM}",
                subject: "Jenkins Build Success: ${env.JOB_NAME}",
                body: """
                        Hello Developer,
                        The Jenkins pipeline for ${env.JOB_NAME} completed successfully
                        Build Details are:
                        ${env.BUILD_INFO}
                        BUILD URL: ${env.BUILD_URL}
                        Console logs: ${env.BUILD_URL}console
                        Artifacts Download: ${env.BUILD_URL}artifact/target/
                        
                        Regards,
                        Jenkins CI Server 
                        DevOps Team
                        """
        }
        failure {
            mail to: 'akshathabm20@gmail.com',
                cc: "${env.DEV_TEAM}",
                subject: "Jenkins Build Failed: ${env.JOB_NAME}",
                body: """
                        Hello Developer,
                        The Jenkins pipeline for ${env.JOB_NAME} has failed
                        Build Details are:
                        ${env.BUILD_INFO}
                        BUILD URL: ${env.BUILD_URL}
                        Console logs: ${env.BUILD_URL}console
                        Artifacts Download: ${env.BUILD_URL}artifact/target/

                        Please check the logs to resolve the issue!
                        
                        Regards,
                        Jenkins CI Server 
                        DevOps Team
                        """
        }
        always {
            echo "Cleaning workspace"
            cleanWs() 
        }
    }
}
              

pipeline {
    

    options {
        disableConcurrentBuilds()
    }

    environment {
        ENVIRONMENT = commonFunctions.getEnvironment()
        ENVIRONMENT_REPORT = commonFunctions.getEnvironmentReport()
    }

    stages {
        // Resto de los stages omitidos por brevedad

        stage('Package and Upload to S3') {
            steps {
                script {
                    def zipFileName = "demo-jenkins.zip" // 3. cambiar el nombre final del zip
                    sh "zip -r ${zipFileName} ."

                    s3Upload(
                        file: zipFileName,
                        bucket: "demo-codedeploy-ml", // 1. cambiar el bucket s3 
                        path: "codedeploy-${getEnvironment()}/", // 2. cambiar el path 
                        force: true
                    )
                }
            }
        }
    }
}


def isProduction() {
  return env.BRANCH_NAME == 'production'
}

def isDevelop() {
  return env.BRANCH_NAME == 'develop'
}

def getEnvironment() {
  if (isDevelop()) {
    return 'dev'
  }

  if (isProduction()) {
    return 'prd'
  }

  return 'dev'
}

node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "bifrost"
    registryHost = "127.0.0.1:30400/"
    imageName = "${registryHost}${appName}:${tag}"
    env.BUILDIMG=imageName

   if (env.BRANCH_NAME == "integration" || env.BRANCH_NAME.startsWith('master'))) {
    stage "Build"
    
        sh "docker build -t ${imageName} -f applications/bifrost/Dockerfile applications/bifrost"
   
    
    stage "Push"

        sh "docker push ${imageName}"
}

   if (env.BRANCH_NAME == "integrator") {
     stage "Deploy"
     
     sh "docker run -d -p 80 --name=bifrost ${imageName}:v1 "

   }

   if (env.BRANCH_NAME == "master") {
    stage "Deploy"

        sh "sed 's#127.0.0.1:30400/bifrost:latest#'$BUILDIMG'#' applications/bifrost/k8s/deployment.yaml | kubectl apply -f -"
        sh "kubectl rollout status deployment/bifrost"
}
}

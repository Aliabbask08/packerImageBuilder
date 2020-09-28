pipeline {
   agent any
   environment{
         AWS_REGION="ap-south-1"
         AWS_PROFILE="myprofile"     
}
   stages {
     stage("Opening"){
         steps{
            //Welcome message
            figlet "Welcome to Jenkins"

}
}  
    stage("Workspace_cleanup){
        //Cleaning WorkSpace
        steps{
            step([$class: 'WsCleanup'])
}
}
   stage("Repo_clone"){
      //Clone repo from GitHub
      checkout ([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[credentialsId: '', url: '']]]) 

}
  stage("Static_Analysis"){
    //validation of packer
     steps{
         script{
             sh "packer validate"
}
}
}
  stage("build_image"){
   //Run packer script to build image
    steps{
        script{
           sh "packer build"

}
}
}
  stage("Test_Build_Image_In_AWS"){
   //Check AMI in AWS account
     steps{
         script{
            sh "aws ami describe --region "${AWS_REGION}"}"

}
}
}
}
}

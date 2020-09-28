pipeline {
   agent any
   environment{
         AWS_REGION="ap-south-1"
         AWS_PROFILE="myprofile"     
}
   stages {
     stage ("Pre-Install"){
        steps {
            script{
               sh "sudo yum install figlet -y"

}
}
}
     stage("Opening"){
         steps{
            //Welcome message
            script{
               sh "figlet "Welcome to Jenkins""
}
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
      checkout ([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[credentialsId: '', url: 'git@github.com:Aliabbask08/packerImageBuilder.git']]]) 

}
  stage("Static_Analysis"){
    //validation of packer
     steps{
         script{
             sh "packer validate -var \"profile=${AWS_PROFILE}\""
}
}
}
  stage("build_image"){
   //Run packer script to build image
    steps{
        script{
           sh "packer build -var \"profile=${AWS_PROFILE}\""

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

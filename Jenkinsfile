pipeline {
   agent any
   environment{
         AWS_REGION="ap-south-1"
         AWS_PROFILE="packer"  
         CONFIG_FILE="ami.json"   
}
   stages {
     stage ("Pre-Install"){
        steps {
            script{
             
               sh "sudo yum install cowsay -y"

}
}
}
     stage("Opening"){
         steps{
            //Welcome message
            script{
               sh "cowsay 'Welcome to Packer'"
}
}
}  
     stage("Workspace_cleanup"){
        //Cleaning WorkSpace
        steps{
            step([$class: 'WsCleanup'])
}
}
   stage("Repo_clone"){
      //Clone repo from GitHub
      steps {
         checkout ([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[credentialsId: 'Jenkins_id', url: 'git@github.com:Aliabbask08/packerImageBuilder.git']]]) 

}
}
  stage("Static_Analysis"){
    //validation of packer
     steps{
         script{
               sh '''
                    echo "This is static Analysis"  
                    sudo packer validate 
'''
}
}
}
  stage("build_image"){
   //Run packer script to build image
    steps{
        script{
          sh '''
                 echo "This is build stage"
	         sudo packer build ${CONFIG_FILE}       
'''
}
}
}
  stage("Test_Build_Image_In_AWS"){
   //Check AMI in AWS account
     steps{
         script{
            //sh "aws ami describe --region "${AWS_REGION}"}"
              sh "echo 'This is test stage'"
}
}
}
}
}

# Unicorn-web-project
In this exercise, you will experience the process of creating a CI/CD pipeline for a Java application deployed onto an EC2 Linux instance. Later you will containerize the application and publish it to Amazon ECR. 

Overall solution includes the following:

- AWS CodeCommit as a Git repository
- AWS CodeArtifact as a managed artifact repository
- AWS CodeBuild as a way to run tests and produce software - packages
- AWS CodeDeploy as a software deployment service
- AWS CodePipeline to create an automated CI/CD pipeline

### AWS CodeBuild
We will setup a CodeBuild project to package our application code into a Java Web Application Archive (WAR) file

1. Create an S3 bucket
2. Create a CodeBuild build project
3. Create the buildspec.yml file in the root of the code repository.
    - Make sure to replace the domain-owner account ID with your own account ID.
4. Modifying the IAM role
    - As we're using CodeArtifact during the build phase, there is a small change required in the auto-generated IAM role for code build to ensure it has permission to use CodeArtifact. Attach the IAM policy `IAM-policies/codeartifact-unicorn-consumer-policy.json`.

### AWS CodeDeploy
1. Create an EC2 instance
2. Create scripts to run the application
3. In the scripts folder of the repository you should see the following files:
    `Install_dependencies.sh`,`start_server.sh`,and`stop_server.sh`
4. Add `appspec.yml` in the root directory of the project:
5. Create CodeBuild service IAM Role
6. Create a CodeDeploy application
7. Create a deployment group
8. Create deployment

### AWS CodePipeline
- Dev Environment
We use CodePipeline to create an automated pipeline using the CodeCommit, CodeBuild, and CodeDeploy components created earlier. The pipeline will be triggered when a new commit is pushed to the main branch of our Git repo.
- Production Environment
After that we need to extend our deployment pipeline to add a manual approval step before deploying to our production environment. For this we need to create/modify the following:
    - Add another EC2 instance
    - Additional CodeDeploy deployment group 
    - Create SNS topic 
    - Update CodePipeline
    - Add approval stage 
    - Add production deployment stage	

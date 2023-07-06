- [JFrog CLI to publish build to Artifactory](#jfrog-cli-to-publish-build-to-artifactory)
  - [Step 1 - Configure the JFrog CLI](#step-1---configure-the-jfrog-cli)
  - [Step 2 - Perform your builds and publishes using JFrog CLI](#step-2---perform-your-builds-and-publishes-using-jfrog-cli)
    - [To upload any files or to deploy your artifacts use the following command](#to-upload-any-files-or-to-deploy-your-artifacts-use-the-following-command)
    - [To do a docker push using JFrog CLI use the following command](#to-do-a-docker-push-using-jfrog-cli-use-the-following-command)
    - [To use git in your build use the following command](#to-use-git-in-your-build-use-the-following-command)
    - [To collect your environment variables during build, use the following command](#to-collect-your-environment-variables-during-build-use-the-following-command)
    - [To publish your build info use the following command](#to-publish-your-build-info-use-the-following-command)
  - [Step 3 - Try it yourself](#step-3---try-it-yourself)

# JFrog CLI to publish build to Artifactory

## Step 1 - Configure the JFrog CLI
- Execute the following command to add your configuration.
    ```jf config add <server-name>```
- It will prompt for some details like your JFrog URL, User Credentials, if you have any reverse proxy configured, weather to allow http if you are using insecure url.
- To verify the configuration is perfectly set, use the following command
    ```jf config show```
  
## Step 2 - Perform your builds and publishes using JFrog CLI
### To upload any files or to deploy your artifacts use the following command
  ```jf rt u [command options] <source pattern> <target pattern>```
- Source Pattern: Specifies the local file system path to artifacts which should be uploaded to Artifactory.
- Target Pattern: Specifies the target path in Artifactory in the following format: repository-name/repository-path.
- 
### To do a docker push using JFrog CLI use the following command
  ```jf rt docker-push ${SERVER_NAME}.jfrog.io/${VIRTUAL_REPO_NAME}/my-docker-image:latest ${VIRTUAL_REPO_NAME} --build-name=<your-name> --build-number=<build-number> --project=<devnext-workshop-{i}>```

### To use git in your build use the following command
  ```jf rt build-add-git <your-name> <build-number> --project <devnext-workshop-{i}>```
- It collects VCS details from git and add them to a build.

### To collect your environment variables during build, use the following command
  ```jf rt build-collect-env <your-name> <build-number> --project <devnext-workshop-{i}>```

### To publish your build info use the following command
  ```jf rt build-publish <your-name> <build-number> --project <devnext-workshop-{i}>```


## Step 3 - Try it yourself
- Test your knowledge by performing a promote in artifactory using cli.
- You can get help by using ```jf rt -h```



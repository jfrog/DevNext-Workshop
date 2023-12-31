- [Working with Artifactory as your docker registry](#working-with-artifactory-as-your-docker-registry)
  - [Prerequisites](#prerequisites)
  - [Step 1 - Update the dockerfile](#step-1---update-the-dockerfile)
  - [Step 2 - Push custom image to your docker repository](#step-2---push-custom-image-to-your-docker-repository)


# Working with Artifactory as your docker registry

## Prerequisites
- Create `Identity Token` from User Profile.
- Navigate to Username -> 'Edit Profile'
- Enter the password to 'Unlock'
- Click on 'Generate an Identity Token' button to create a token.

## Step 1 - Update the dockerfile  

- Update the dockerfile present in this repository. Update the FROM line of the Dockerfile to reference your virtual Docker repository.
    - ```FROM ${SERVER_NAME}.jfrog.io/${VIRTUAL_REPO_NAME}/alpine:3.11.5```

    - eg :- ``` FROM psapac.jfrog.io/dnw1-devnext-docker-stage/alpine:3.11.5```
      
    - The SERVER_NAME is the first part of the URL given to you for your environment: ```https://<SERVER_NAME>.jfrog.io.``` You can also get this information from the docker login command.
  
    - Start the Docker Engine if not started. 

      <img src="/01-artifactory-essentials/images/docker-command.png" alt="docker commands" style="height: 100px; width:100px;"/>

    - The VIRTUAL_REPO_NAME is the name ““jfrog-docker” that you assigned to your virtual repository in Stage 2.

    - After modifying your dockerfile should be something like below.

      <img src="/01-artifactory-essentials/images/modified-dockerfiles.png" alt="dockerfile" style="height: 100px; width:100px;"/>
    
## Step 2 - Push custom image to your docker repository

- Login to your docker virtual repository. Replace the  SERVER_NAME and VIRTUAL_REPO_NAME as mentioned in above step.
    - ``` $ docker login ${SERVER_NAME}.jfrog.io```
    - eg :- ``` docker login psapac.jfrog.io ```
      
      <img src="/01-artifactory-essentials/images/login-docker.png" alt="docker login" style="height: 100px; width:100px;"/>
      
- Build your docker image. Replace the  SERVER_NAME and VIRTUAL_REPO_NAME as mentioned in above step.
    - ```$ docker build -t psapac.jfrog.io/dnw1-devnext-docker-stage/jfrog-docker-image:1.0.7 . ```
      
      <img src="/01-artifactory-essentials/images/docker-builds.png" alt="docker build" style="height: 100px; width:100px;"/>
      
- Push the build docker image to your docker registry. Replace the  SERVER_NAME and VIRTUAL_REPO_NAME as mentioned in above step. 
    - ``` $ docker push psapac.jfrog.io/dnw1-devnext-docker-stage/jfrog-docker-image:1.0.7 ```
      
      <img src="/01-artifactory-essentials/images/dockerpush.png" alt="docker push" style="height: 100px; width:100px;"/>


# Shoe-Shopping

Shoe Shopping Cart built with SpringBoot, JPA, MySQL , Spring Security, Hibernate and Thymeleaf

![image](https://user-images.githubusercontent.com/29988949/75882730-9ad11680-5dd6-11ea-9648-252426582a96.png)

![image](https://user-images.githubusercontent.com/29988949/75947593-c6dfac80-5e55-11ea-8582-bce667beb9bb.png)

`ProductList Page`

![image](https://user-images.githubusercontent.com/29988949/75968115-bf35fd00-5e81-11ea-9bae-e78ff047dcfd.png)

`Cart Page`

![image](https://user-images.githubusercontent.com/29988949/75956013-da960d80-5e6b-11ea-84b2-a0ca854ef9c9.png)


# Deploy Shoe-Shopping application using Docker & GitLab CI/CD

## Step 1: Create a GitLab repository

Create a [blank GitLab project](https://docs.gitlab.com/ee/gitlab-basics/create-project.html), 
push your project from local machine to GitLab. After that you will probably get something like that
![Project structure](https://pp.userapi.com/c850224/v850224063/1058e3/tEToCCj-dBk.jpg)

For the guide I will use following project URL:

`https://gitlab.com/your_username/your_project_name/`

You have to replace `your_username` and `your_project_name` in the source code to make it work. 

## Step 2: Create a Dockerfile

The second step is creating a Java & Maven image. A Docker image is a file, comprised of multiple layers,
 used to execute code in a Docker container. A Docker image is described in `Dockerfile` by default. The most interesting commands is:
 [Dockerfile](https://github.com/Cuong02/Shoe-shop/blob/main/docker_file.png)
 is used to set a default command for the image. However it will be over-written by a Docker-compose file.

## Step 3: Create GitLab CI/CD pipeline

For my purposes contains only 2 basic steps: 
* `build` step builds Java application image and push it to a private registry. Substitute a registry URL by your own link.
* `deploy` step logins to a server via ssh and pulls changes from registry

The deploy step uses a `devops/deploy.sh` file. You have to change it: replace **47.47.47.47** to your remote address IP
and replace registry URL:
> docker pull registry.gitlab.com/your_username/your_project_name:latest

## Step 4: Push new files

Push all new files and directories (`Dockerfile`, `docker-compose.yml`, `.gitlab-ci.yml`, `devops/`) to the branch `master`.

## Step 5: Generate SSH keys

Locally run a command `ssh-keygen -t rsa`, it will prompt you to enter passphrase - **leave it blank**. 
The command generates two files with two keys: public and private. 

Copy the public key to your server `~/.ssh/authorized_keys` file.

Also you must to set a CI/CD environment variable called `DEPLOY_KEY` to your private key. 
Go to **GitLab project page - Settings - CI / CD - Environment variables** and create a variable 
![Set variable](https://pp.userapi.com/c854120/v854120736/8f3a/C-NCoEPFCBg.jpg)

`git clone https://gitlab.com/your_username/your_project_name.git`

## Step 9. Make a commit to prove that everything works fine

Or create an issue to make me now that the guide has a mistake

# How to use fiware-testbed-deploy for deploying a phonehome VM with Docker

A set of scripts to create a virtual machine required for PhoneHome service. The
environment is created in a virtual machine using a Cloud infrastructure.

----
## 1. Generating docker image
Docker allows you to deploy a fiware-phonehome container, which deploys a VM with a Cloud infrastructure in a few minutes.
This method requires that you have installed docker or can deploy container into the FIWARE Lab (see previous details about it).

  1. Download [fiware-testbed-deploy' source code](https://github.com/telefonicaid/fiware-testbed-deploy) from GitHub (`git clone https://github.com/telefonicaid/fiware-testbed-deploy.git`)
  2. `cd fiware-testbed-deploy/docker/DeployPhoneHome`

Then, you just need to create a new docker image executing `docker build -t fiware-phonehome -f Dockerfile .`. Please keep in mind that if you do not change the name of the image
 it will automatically update an existing one.

To see that the image is created run `docker images` and you see something like this:

    REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
    fiware-phonehome          latest              103464a8ede0        30 seconds ago      551.3 MB


----
## 2. Running docker image
Now is time to execute the container.  Previously you should configure a set variables with the
 FIWARE Lab (or a Cloud) credentials. You have to define the following environment variables:

    export OS_AUTH_URL=<the authentication URL for the keystone in the Cloud>
    export OS_USERNAME=<a user with an account in the Cloud>
    export OS_TENANT_NAME=<a project name from the account in the Cloud>
    export OS_PASSWORD=<the password for an account in the Cloud>
    export OS_REGION_NAME=<the region name>
    export OS_USER_DOMAIN_NAME=<OpenStack user domain name>
    export OS_PROJECT_DOMAIN_NAME=<OpenStack project domain name>
    export BOOKED_IP=<a booked IP in your Cloud infrastructure to deploy the VM>

To run the container just execute:

    docker run -e OS_AUTH_URL=$OS_AUTH_URL -e OS_USERNAME=$OS_USERNAME -e OS_TENANT_NAME=$OS_TENANT_NAME -e OS_PASSWORD=$OS_PASSWORD -e OS_REGION_NAME=$OS_REGION_NAME -e  OS_USER_DOMAIN_NAME=$OS_USER_DOMAIN_NAME -e OS_PROJECT_DOMAIN_NAME=$OS_PROJECT_DOMAIN_NAME -e BOOKED_IP=$BOOKED_IP -e Region1=$Region1 fiware-phonehome

----
## 3. Running with docker-compose
 This time, we take advantage of the docker compose.  Previously you should configure a set variables with the
 FIWARE Lab (or a Cloud) credentials. You have to define the following environment variables:

    export OS_AUTH_URL=<the authentication URL for the keystone in the Cloud>
    export OS_USERNAME=<a user with an account in the Cloud>
    export OS_TENANT_NAME=<a project name from the account in the Cloud>
    export OS_PASSWORD=<the password for an account in the Cloud>
    export OS_REGION_NAME=<the region name>
    export OS_USER_DOMAIN_NAME=<OpenStack user domain name>
    export OS_PROJECT_DOMAIN_NAME=<OpenStack project domain name>
    export BOOKED_IP=<a booked IP in your Cloud infrastructure to deploy the VM>
    export Region1=<the name for the region of the Cloud to be deployed>

Just execute `docker-compose up` to launch the architecture. You can take a look to the log generated executing `docker-compose logs`. You will see
that a VM will be deployed and some software is installed.

----
## 4. Other info

Things to keep in mind while working with docker containers and fiware-testbed-deploy.

### 4.1 Data persistence
Everything you do with fiware-testbed-deploy when dockerized is non-persistent. *You will lose all your data* if you turn off the fiware-testbed-deploy container. This will happen with either method presented in this README.

### 4.2 Using `sudo`

If you do not want to have to use `sudo` follow [these instructions](http://askubuntu.com/questions/477551/how-can-i-use-docker-without-sudo).




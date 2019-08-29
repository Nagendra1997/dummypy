---
description: Mesibo On-Premise Server
keywords: open, source, contributing, overview, on-premise
title: Installing & Running Mesibo On-Premise Server
---
Mesibo On-Premise solution allows you to run the entire Mesibo solution in your own premise / data center. All the messages and calls goes through your own data center and stay in your own database. All you have to do it to download Mesibo on-premise server image and run it in your own data center. That's it! 

Mesibo On-Premise is the perfect solution for ultimate control over your sensitive data.We have also released the entire source code of Mesibo Android and iOS [sample apps](https://github.com/mesibo/samples) on GitHub, which is continuously updated. You can download the entire source code, and customize it to suit your needs. 

### Features
- All the mesibo features, including Messaging, Voice and Video calling
- Complete control over your data. All the messages and calls route through and stays in your own infrastructure. 
- Unlimited storage and data retention
- Unlimited Messages
- Private and public deployment
- Auto fallback to cloud as a backup, if required. 
- Push notifications
- At no additional cost

### Prerequisites
It is required that you are familar with:

- mesibo API and successfuly using Mesibo cloud services. If not, please refer to Mesibo 
[getting started](https://mesibo.com/documentation/get-started/) guide and tutorials before setting up On-Premise server.

- setting up a Linux server and MySQL database. If not, refer to online tutorials for the Linux distribution of your choice. 

- setting up Docker and using Docker images. If not, refer to excellent Docker documentation and various online tutorials on docker. 


### Requirements
Mesibo made it extremely simple for you to setup an On-Premise Messaging, Voice and Video call server. You only need to provide bare minimum infomation regarding your setup and network and rest will be taken care by Mesibo. 

Mesibo only requires the following:

- Linux 64-bit server (or an instance) with at least 1GB free RAM. Mesibo supports all the major Linux distributions, including: 

	- RHEL or CentOS 7.x 

	- Ubuntu 16.x or 18.x

	- Fedora 28 or 29

	- Debian 9 or 10

	- SLES 15

	- Oracles Linux 7.x

- MySQL (or MariaDB) database 



## Step 1 - Install Docker
Mesibo On-Premise server is distributed as a docker image so that you can install it on most Linux distributions without worrying about any dependencies etc. All you need is to install Docker to run it. If you have already installed Docker on your server, you can skip to Step 2. 

You can install Docker by running the command below.

```
$ sudo curl -sSL https://get.docker.com/ | sh
```

Once Docker is installed, you need to start the Docker daemon. Most Linux distributions use `systemctl` to start services. If you
do not have `systemctl`, use the `service` command.

- **`systemctl`**:

  ```bash
  $ sudo systemctl start docker
  ```

- **`service`**:

  ```bash
  $ sudo service docker start
  ```

Once the installation is over, you can verify it by running 

```
$ sudo docker run hello-world
```

## Step 2 - Download Mesibo On-Premise Server Image
Download Mesibo On-Premise server by running the following command

```
$ sudo docker pull mesibo/mesibo
```

However, before we launch Mesibo, we need to setup a mesibo configuraiton file. 

## Step 3 - Configure Mesibo
Mesibo requires following configuration:

- Mesibo App Token, which you can get from Mesibo Console

- Database Information

- Your Hostname. All your users will connect to this hostname and hence ensure that it is correct.

- TLS/SSL Cerificate for your hostname [Optional but recommended]


## Step 3 - Configure TLS Certificate
Although Mesibo can automatically generate a self-signed certificate for you, it is recommended that you configure a valid certificate. You can use any existing ceriticate, OR Letsencrypt which is a free service OR any other provides of your choice to get a secure ceritificate. Note that, wild card certificate is not recommended. 

## Step 3 - Run Mesibo

You need to specify the app token which needs to be run on-premise,to the mesibo instance.
The app token can be obtained from mesibo console which looks like the following 
```
**cn9cvk6gnm15e7lrjb2k7ggggax5h90n5x7dp4sam6kwitl2hmg4cmwabet4zgdw**    

```
![App token Mesibo Console](https://mesibo.com/documentation/tutorials/first-app/images/app-token.jpg)

In the below command Replace APP_TOKEN with the your app token that you got from console and then run it.

```
docker run -p 5222:5222 -p 5228:5228 -p 80:80 -p 443:443 -p 4443:4443 -p 5443:5443 -p 513:513 -d mesibo/mesibo APP_TOKEN
```
The logs can be read using the following command 
where CONTAINER is the container ID
```
docker logs CONTAINER
```

The logs should look like below:
```
: MySQL: connection opened
: Starting Mesibo

``` 

Now, check Running status of your server from Mesibo Console --> App Settings --> On Premise Hosting. If successfull the running status field will contain your hostname , otherwise it will contain "Not running"


![Console Screenshot](mesibo.com)

If your on-premise server is setup and running mesibo continue else refer to [troubleshooting](mesibo.com)



## Step 3 - Firewall


## Step 4 - Group Management


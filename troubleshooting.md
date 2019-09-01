## A troubleshooting guide to setting up Mesibo On-Premise

1. Please ensure that you have downloaded the latest version of 
Mesibo Server Image
To update your docker image:
```bash
sudo docker pull mesibo/mesibo
```
2. Before you run Mesibo docker container ensure you have correctly configured your application as per your requirements in the [console](https://mesibo.com/console). Refer to Step-3 in the [documentation](mesibo-on-premise-link)
 
3. You need to pass your app token to Mesibo instance when you run it. Verify that this App Token is the correct on and it belongs to the application you have configured in the console.

4. To view logs for the Mesibo container you are running

```
sudo docker logs <CONTAINER_ID>
```
To get the CONTAINER_ID of the docker container you are running 
```
sudo docker ps
```

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                                                                                                                            NAMES
4fd84018a651        mesibo/mesibo       "/usr/bin/mesibo_onp…"   56 minutes ago      Up 56 minutes       0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp, 0.0.0.0:513->513/tcp, 0.0.0.0:4443->4443/tcp, 0.0.0.0:5222->5222/tcp, 0.0.0.0:5228->5228/tcp, 0.0.0.0:5443->5443/tcp   modest_mendeleev

```
for container 4fd84018a651 you can get the logs using

```
sudo docker logs 4fd84018a651 
```

Now,the log output should like so
```
E3108-082633-480 (1): Mesibo Build: Aug 29 2019 15:39:08
E3108-082633-506 (1): PID: 1
E3108-082633-775 (1): Local IP Address: 172.17.0.2
E3108-082634-580 (10): *** onp_message: On-Premise not enabled - login to Mesibo console to enable it
E3108-082634-639 (10): Generating TLS certificate for 192.168.0.107
I3108-082635-167: Starting mesibo

```

5. Once you have verified that your log output is as expected, only then turn on the On-Premise switch in the console.


You may get unexpected errors/issues during setup. Please follow the steps accordingly to resolve these issues.

-Getting ERROR docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock

Check if the docker daemon running. 
Once Docker is installed, you need to start the Docker daemon. Most Linux distributions use `systemctl` to start services.If you do not have `systemctl`, use the `service` command.

- **`systemctl`**:

  ```bash
  $ sudo systemctl start docker
  ```

- **`service`**:

  ```bash
  $ sudo service docker start

To verify that your docker daemon is running try
```
$ sudo docker run hello-world
```
which should output
```
Hello from Docker!
This message shows that your installation appears to be working correctly.

```

-Getting ERROR docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock
Ensure that you are running all docker commands with the prefix sudo(with security privelages)
For example,
```
sudo docker pull mesibo/mesibo
```

- I have configured my app correctly and I am running Mesibo Container. But,my logs do not indicate anything when a user logs in.
Your server is not connected to your application. Your logs will contain an entry that says
```
 *** onp_message: On-Premise not enabled - login to Mesibo console to enable it
```
Turn on the Enable On-Premise switch and your app connection should get redirected to your server immediately!



- Getting Error: MySQL Connection Failed -- Can't connect to MySQL server in server logs 
1.Check your databse host address ,hostname and other details is matching to the details you have entered in console.
2.  Please check you have granted the necessary permissions to access your database from your hostname address.
3. Check your firewall configuration and ensure that is configured properly for allowing connections from your hostname address. (You can use the tool iptables to check your firewall configuration)
4. Stop your docker container and then start it.

-Getting Error: Unable to verify app token - network error in server logs
Check your firewall configuration and verify it is configured to allow connections from your host server.Then,stop your docker container and then start it.

- How can I stop the docker container running Mesibo?
Get the CONTAINER_ID of the docker container you are running using
```
sudo docker ps
```
Now,to stop this container use
```
sudo docker stop <CONTAINER_ID>
```



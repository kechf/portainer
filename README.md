# Installation on Windows 10
1. Open the Docker Menu on the right side of the Windows Taskbar and go to Settings (3rd. Option). 

 ![](C:\dev.git\portainer\open_docker_settings.png)

2. On the Tab general, activate the option Expose daemon on tcp://localhost:2375 without TLS (last Option). 

![](C:\dev.git\portainer\docker_settings.png)



3. Then, open a PowerShell with administrator rights and type the following:

```sh 
netsh interface portproxy add v4tov4 listenaddress=10.0.75.1 listenport=2375 connectaddress=127.0.0.1 connectport=2375

netsh advfirewall firewall add rule name="docker management" dir=in action=allow protocol=TCP localport=2375
```

The first line connects 10.0.75.1:2375 to the daemon socket on 127.0.0.1:2375, and the second line adds a pass-through on the firewall for the port 2375 (*) . You need to know that this makes yourself vulnerable to remote code execution attacks.

Then, start the Portainer container using an user-mode PowerShell (you do not need administrator rights to do this) typing: 

```sh
docker-compose up -d
```



Go to your browser and type http://localhost:9000 and configure your admin user and password if needed.
# spring_boot_as_ubuntu_service
Deploying Spring Boot app as a Linux | Ubuntu  service





Anyways, to create a Linux daemon the systemd way:

#Create a service file in /etc/systemd/system. Let's call it javaservice.service. Let the contents be:
------------------------------------------------------------------------------------------------------------
[Unit]
Description=My Java Service

[Service]
User=root 
#The configuration file application.properties should be here:
WorkingDirectory=/home/myuser/my-apps (only folder path)
ExecStart=/usr/bin/java -Xmx256m -jar applicationname.jar --server.port=9900
SuccessExitStatus=143
TimeoutStopSec=10
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
-------------------------------------------------------------------------------------------------------------------------

1 .<== notifies systemd of the new service file .

sudo systemctl daemon-reload   

2.<== enable it so it runs on boot 2.

sudo systemctl enable javaservicename.service		   


3.javaservice.service will be added to the dir /etc/systemd/system/multi-user.target.wants. This dir indicates what services to start on boot

sudo systemctl start javaservicename 

4.check that the service is running fine 4.

sudo systemctl status javaservicename   

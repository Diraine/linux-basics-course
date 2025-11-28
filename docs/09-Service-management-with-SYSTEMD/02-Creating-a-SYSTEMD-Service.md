# Creating a SYSTEMD Service

In this guide, we detail how to manage services with SYSTEMD by building a service unit from scratch. We will utilize essential SYSTEMD utilities—specifically, systemctl and journalctl—and conclude with a hands-on lab exercise.

Bob’s requirements for the service are as follows:

- A shell script named project-mercury.sh located in /usr/bin must execute as a background service.
- The service should be enabled to start automatically during boot.
- The script launches a Python Django application that depends on a PostgreSQL database; therefore, PostgreSQL must be running prior to the application's start.
- The service must run under a pre-created account called project_mercury rather than the default root user.
- In case of application failure, the service should restart automatically, waiting 10 seconds between attempts.
- The service must not restart automatically if it is manually stopped by an administrator.
- All service events—including start, stop, and errors—must be logged for later analysis.
- The service should adhere to the graphical.target since Bob’s system defaults to a graphical environment.
Bob’s colleague, Dave, recommends constructing the service unit file in gradual steps. Follow along with the steps below.

---


### Step 1. Creating the Basic Service Unit

Begin by defining a basic service unit file named project-mercury.service under the /etc/systemd/system directory. Initially, the unit file only needs to execute the command in the background using /bin/bash because project-mercury.sh is a Bash script.

Below is the minimal service unit definition:

```
[Service]
ExecStart=/bin/bash /usr/bin/project-mercury.sh
```

To start the service in the background, run the following command (using sudo if necessary):

```
sudo systemctl start project-mercury.service
```

Verify that the service is active with:

```
sudo systemctl status project-mercury.service
```

A sample output might look similar to:

```
● project-mercury.service
   Loaded: loaded (/etc/systemd/system/project-mercury.service; static; vendor preset: enabled)
   Active: active (running) Fri 2020-04-10 00:52:16 EDT; 6min ago
 Main PID: 25041 (project-mercury.sh)
   Tasks: 2 (limit: 4915)
   CGroup: /system.slice/project-mercury.service
           ├─6494 sleep 60
           └─25041 /bin/bash /usr/bin/project-mercury.sh
```

After verifying, you can stop the service by running:

```
sudo systemctl stop project-mercury.service
```
---


### Step 2. Enabling the Service on Boot

To automate the start of the service during boot, add an [Install] section to the service unit file. The WantedBy directive ties the service to the graphical target, which corresponds to the current runlevel.

Update your service unit file as follows:

```
[Service]
ExecStart=/bin/bash /usr/bin/project-mercury.sh

[Install]
WantedBy=graphical.target
```
---


### Step 3. Running the Service Under a Specific User

By default, services run as root. To have the service operate under the project_mercury account, include the User directive within the [Service] section:

```
[Service]
ExecStart=/bin/bash /usr/bin/project-mercury.sh
User=project_mercury


[Install]
WantedBy=graphical.target
```

> 💡 **Note**

> Using a dedicated service account improves security by limiting the permissions available to the service.

---


### Step 4. Configuring Automatic Restarts

Configure the service to restart automatically if it fails. Use the Restart directive set to on-failure and specify a 10-second delay between restart attempts using RestartSec:

```
[Service]
ExecStart=/bin/bash /usr/bin/project-mercury.sh
User=project_mercury
Restart=on-failure
RestartSec=10


[Install]
WantedBy=graphical.target
```

SYSTEMD logs all service events (start, stop, and failures) by default, so no extra logging configuration is required.

---


### Step 5. Defining a Dependency on the PostgreSQL Service

Since the Python Django application depends on a PostgreSQL database, ensure that project-mercury.service starts only after PostgreSQL is active. To achieve this, add a [Unit] section that includes a description, a documentation URL, and the After directive to express the dependency:

```
[Unit]
Description=Python Django for Project Mercury
Documentation=http://wiki.caleston-dev.ca/reported
After=postgresql.service


[Service]
ExecStart=/bin/bash /usr/bin/project-mercury.sh
User=project_mercury
Restart=on-failure
RestartSec=10


[Install]
WantedBy=graphical.target
```

After updating the service unit file, reload the systemd daemon to apply the changes:

```
sudo systemctl daemon-reload
```
---


### Final Service Unit File

Below is the complete service unit file that fulfills all the specified requirements:

```
[Unit]
Description=Python Django for Project Mercury
Documentation=http://wiki.caleston-dev.ca/reported
After=postgresql.service


[Service]
ExecStart=/bin/bash /usr/bin/project-mercury.sh
User=project_mercury
Restart=on-failure
RestartSec=10


[Install]
WantedBy=graphical.target
```
> 💡 ***Deployment Tip***

> Bob intends to replicate these steps on the development server, ensuring the Python Django application and PostgreSQL database are configured reliably and efficiently with SYSTEMD.

---


### Starting and Verifying the Service

With the final configuration in place, start the service by running:

```
sudo systemctl start project-mercury.service
```

Then, confirm its status with:

```
sudo systemctl status project-mercury.service
```

This completes the configuration of the SYSTEMD service for project-mercury. Enjoy a more automated and robust service deployment!



1. In this lab, we will secure the development environment by utilizing `iptables`. <br> Whenever necessary, utilize `sudo` to execute commands as the root user. Please note that Bob's password is `caleston123`.

2. Below is the simple architecture diagram of the implementation, <br> which represents a two-tier application.

- The web server is hosted on devapp01.
- The database server is hosted on devdb01.
- The software repository is hosted on caleston-repo-01.
Here are the connectivity requirements:

1. SSH access must be enabled from Bob's laptop to both the Web and DB servers.<br>
2. The Web Server must be accessible from Bob's laptop via HTTP/80.<br>
3. The Web Server should have access to the Software Repository server on port 80.
![architecture-diagram](https://zwlxuq2lideay7t2.labs.kodekloud.com/images/iptables-arch.png)



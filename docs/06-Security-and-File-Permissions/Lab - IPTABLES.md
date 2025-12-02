
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

3. Install iptables on both `devapp01` and `devdb01` servers.

Instructions:

SSH into each server as the user bob.
Switch to the root shell to avoid repeated password prompts.
Update the package list.
Install iptables.
(Optional) Verify the installation.


4. Check if there are any existing `iptables` rules configured on either the Web Server (`devapp01`) or the DB Server (`devdb01`).

Instructions:

SSH into both `devapp01` and `devdb01` as the user bob.
List the current `iptables` rules on each server.
 `sudo iptables -L`
Determine whether any rules are present.

```
Bob’s password is caleston123.
Use sudo -s after logging in to switch to a root shell and avoid entering the password multiple times.
Use the following command to list all current iptables rules:
iptables -L
If you see only the default policy lines (e.g., "Chain INPUT (policy ACCEPT)"), then no custom rules have been added yet.
```

5. On the Web Server (`devapp01`), add incoming firewall rules to permit SSH and HTTP connections from Bob's Laptop.

Bob's Laptop IP address: `172.16.238.187`

Instructions:

SSH into `devapp01` as the user bob.
Add `iptables` rules to allow:
SSH (port 22) from Bob's Laptop
HTTP (port 80) from Bob's Laptop
Ensure you use the correct source IP and destination ports
***Note :*** Always add ACCEPT rules for allowed traffic before adding any DROP rules to avoid losing your connection.

```
Bob’s password is caleston123.
Use sudo -s after logging in to switch to a root shell and avoid entering the password multiple times.
Use the following commands to add the required rules:
sudo iptables -A INPUT -p tcp -s 172.16.238.187 --dport 22 -j ACCEPT

sudo iptables -A INPUT -p tcp -s 172.16.238.187 --dport 80 -j ACCEPT
Always add ACCEPT rules for allowed traffic before adding any DROP rules to avoid losing your connection.
```
6. Now, lock down incoming traffic on `devapp01` by dropping all incoming connections from any source, on any destination port, for any protocol (TCP/UDP).

Instructions:

SSH into `devapp01` as the user bob.
Switch to the root shell to avoid repeated password prompts.
Add a rule to drop all remaining incoming connections.
Note: Make sure you have already added ACCEPT rules for SSH and HTTP from Bob's Laptop (`172.16.238.187`) before adding this DROP rule, or you may lose your connection.

```
Use the following command to drop all incoming connections:
iptables -A INPUT -j DROP
This rule should be added after your ACCEPT rules, so it appears at the bottom of the INPUT chain.
Bob’s password is caleston123.
If you lose your connection after applying the DROP rule, you may need to restart the lab or open a new terminal.
```

7. On `devapp01`, configure outgoing firewall rules as follows:

Permit outgoing access to:
Port `5432` (PostgreSQL) on `devdb01` (`172.16.238.11`)
HTTP (port `80`) on `caleston-repo-01` (`172.16.238.15`)
Block all other outgoing traffic to HTTP (port 80) and HTTPS (port 443) on any destination.

Instructions:

SSH into `devapp01` as the user bob.
Switch to the root shell to avoid repeated password prompts.
Add the ACCEPT rules for the specific destinations and ports before adding the DROP rules.
Add the DROP rules for outgoing HTTP and HTTPS traffic.
Verify the rules are in the correct order: ACCEPT rules should come before DROP rules.

```
Use these commands to add the required rules:
iptables -A OUTPUT -p tcp -d 172.16.238.11 --dport 5432 -j ACCEPT

iptables -A OUTPUT -p tcp -d 172.16.238.15 --dport 80 -j ACCEPT

iptables -A OUTPUT -p tcp --dport 80 -j DROP

iptables -A OUTPUT -p tcp --dport 443 -j DROP

Always add ACCEPT rules before DROP rules to avoid blocking permitted traffic.

Bob’s password is caleston123.

(Optional) Use iptables -L -v --line-numbers to verify rule order.
```

8. On `devapp01`, add an OUTPUT rule at the top of the chain to allow HTTPS (port 443) connections to `google.com.`

Instructions:

SSH into `devapp01` as the user bob.
Switch to the root shell to avoid repeated password prompts.
Insert the rule at the top of the OUTPUT chain to allow outgoing HTTPS traffic to `google.com`.

```
Use the following command to insert the rule at the top of the OUTPUT chain: sudo iptables -I OUTPUT -p tcp -d google.com --dport 443 -j ACCEPT
The -I flag inserts the rule at the top, ensuring it takes precedence over any DROP rules.
Bob’s password is caleston123.
```


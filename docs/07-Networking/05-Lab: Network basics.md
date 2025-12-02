1. Which IP addresses are assigned to Bob's Laptop on its primary network interfaces ?

Run: `ip a` on Bob's Laptop and look for the `inet` IP addresses on interfaces named `eth0` and `eth1.`

Ignore the `lo` interface (`127.0.0.1`) and `eth2` (`172.17.x.x`, used by Docker). The addresses should start with `172.16..`

2. What is the name of the interface that has the IPs (from the previous question) address assigned?

Run: `ip a` and check the interfaces to which the IP's are assigned or
Run: `ip link`

3. What is the `default` gateway configured in the system?
Run the command `ip r` to view your routing table. <br> The default entry will display the `gateway IP address` utilized for directing traffic beyond the local network.


5. We have an apache server which should be accessible at hostname `devapp01-web`. <br> This server runs on `port 80` and should be accessible from Bob's laptop.

6. Check if you are able to connect to the HTTP port 80 on the server devapp01-web from Bob's laptop?
Run: `telnet devapp01-web 80` and check if it's successful.

8. Are you able to ping devapp01-web server?
```
Run: ping devapp01-web
```
9. Luckily, this webserver has two interfaces. The second interface is on another network and is identified by the name devapp01. Check if you are able to ping devapp01
```
Run: ping devapp01
```
10. Let's troubleshoot from the other end. SSH to the webserver by running ssh devapp01
`password caleston123`

12. Inspect the interface eth0 on devapp01, is it UP?

run: `ip link` and look at the status of the interface starting with `eth0`

13. Bring up the eth0 interface
```
Run: sudo ip link set dev eth0 up
```

14. While we are at it, there is also a missing `default route` on the server `devapp01`.

Add the default route via eth0 gateway.

To enable external connectivity, your system needs a default route pointing to your network gateway. `Run:
sudo ip r add default via 172.16.238.1`


17. 

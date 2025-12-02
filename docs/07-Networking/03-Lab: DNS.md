
1. What is the IP address of the DNS Server used in this system?

```
Run: `cat /etc/resolv.conf` and look for the line starting with `nameserver.`
The IP after `nameserver` is the DNS server used by the system.
```
2. Which file is responsible for host file-based DNS resolution?
```
/etc/hosts
```
3. What is the configuration file used for the DNS Server?
```
/etc/resolv.conf
```
4. Change the DNS Server to Google's DNS, which is 8.8.8.8.
```
Edit the file located at /etc/resolv.conf
and update the nameserver IP address to 8.8.8.8.
```
5. What is the current order used by the system to resolve an IP address?
```
grep hosts /etc/nsswitch.conf
```
6. Change the order of resolution to DNS first and then hosts.
```
open the file /etc/nsswitch.conf in a text editor. locate the line starting with hosts:,
and update it to hosts:   DNS files to change the order to DNS first and then hosts.
```
7. Which search domain is configured in this system?
```
inspect the /etc/resolv.conf file and look for the line starting with search
```



1. Which IP addresses are assigned to Bob's Laptop on its primary network interfaces ?

Run: `ip a` on Bob's Laptop and look for the `inet` IP addresses on interfaces named `eth0` and `eth1.`

Ignore the `lo` interface (`127.0.0.1`) and `eth2` (`172.17.x.x`, used by Docker). The addresses should start with `172.16..`

2. 


1. This lab requires some commands to be run as the `root` user. Always use sudo. <br> Bob's default password is `caleston123`

2. What type of account does Bob use?
```
Bob falls into the category of a user. Hence, the most appropriate answer is User Account.
```
3. Which of the following commands will show you the `UID for a user`?
```
Run: id
```

4. What is the UID for bob?
```
Run the id command and look for the UID number
```
5. What level of sudo access does bob have in this system?
```
Run: `sudo grep bob /etc/sudoers`. Bob has `ALL` permissions (4th field)
```
6. A user called chris has been created. <br> Can you find out his Full Name?
```
Inspect the password file: `sudo grep chris /etc/passwd`
```
7. Which groups are chris part of?
```
Run: id chris
```
8. What is chris's primary group?
```
from the `id chris` command, find the group associated with the GID
```
9. Now, lets create a new user called `sarah`. Once done, set her password to `caleston321`
```
Run: `sudo useradd sarah`
and then `sudo passwd sarah` to change the password.
```
10. Create a group called `john` with the `GID 1010`. <br> Next create another user called `john` <br> with `UID = 1010`, p`rimary group = john` and `login shell = /bin/sh`
```
Run: sudo groupadd -g 1010 john
sudo useradd -u 1010 -g 1010 -s /bin/sh john
```






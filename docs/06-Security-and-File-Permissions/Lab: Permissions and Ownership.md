
### info
1. This lab requires some commands to be run as the root user. Always use sudo. <br> Bob's default password is caleston123

2. A new directory called `sports` has been created in your home directory. Inspect it. <br> What is the permission set for the `owner` of this directory?

```
Run: `ls -ld /home/bob/sports` and look at the permissions set for the owner.

`rwx` means the owner has full permissions to `read, write and execute`
```
3. What is the permission set for group users for the same directory sports?
4. What are the permissions set for other users for the sports directory?

```
Run: l`s -ld /home/bob/sports` and look at the permissions set for others.
--- means no permissions set for others!
```
5. Who's the owner of this directory?
6. A new file called `soccer` has been created under the `sports` directory. <br> It has full permissions, update the file so that the group and others only have `read` and `execute` permissions.

```
use: chmod 755 /home/bob/sports/soccer or
chmod go-w /home/bob/sports/soccer
```
7. Now, `add` back the `write` permission for group and `remove all` permission for others for the same file called `soccer`.

```
use: chmod 755 /home/bob/sports/soccer or
chmod go-w /home/bob/sports/soccer
```
8. Now, change the ownership of the file called `soccer` to the `service account` called `mercury`.

```
Use: sudo chown mercury /home/bob/sports/soccer
```
9. We have created another file in the `sports` directory. Change the ownership for the entire `sports` directory including all the files inside to the service account `mercury`.
Try to do this with one single command. Explore the `-R` recursive flag with the `chown` command.

```
run: sudo chown -R mercury /home/bob/sports
```




   

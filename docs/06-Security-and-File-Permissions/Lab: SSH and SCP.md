
1. Which port number does the SSH service use by default? <br> Bob's default password is caleston123
```
SSH makes use of port 22.
You can also validate this by running `netstat -ntlp | grep ssh` on a server running SSH service.

```
2. If you run ssh devapp01 in the terminal, which user are you using to connect to the server?
`bob`
3. Now, let's set up password-less ssh between Bob's laptop and the Dev Application server devapp01. <br> We will make use of bob's user account that has been created in the application server.

4. First, generate the SSH key-pair using the `ssh-keygen` command in the `caleston-lp10` server. <br> Key Type - `RSA`

```
Run: ssh-keygen -t rsa
Use all default options by keying in enter whenever prompted.
use /home/bob/.ssh/id_rsa. to chose path for key whenever prompted
```

5. The public key created using the previous command is:

```
SSH keys are created under .ssh directory under the home directory.
The public key has an extension of .pub
```
6. Copy the public key to the target server `devapp01`. <br> Make use of the `ssh-copy-id` command

```
Run: ssh-copy-id bob@devapp01
ssh-copy-id command should be run without sudo
```

7. Which file on the target server is the public key copied in to?

```
The public key is added to the authorized_keys file
under /home/bob/.ssh directory which is /home/bob/.ssh/authorized-keys
```
8. Finally, copy the file /home/bob/caleston-code.tar.gz from Bob's laptop to the server devapp01 <br> Copy the file to Bob's home directory.

```
Run: scp /home/bob/caleston-code.tar.gz devapp01:/home/bob
```
   



# Lab - Linux Bash Shell

- Access Hands-On Labs here [Hands-On Labs](https://kodekloud.com/topic/lab-linux-bash-prompt/)

1. To check the default shell for the current user. Display the shell for the current user but not necessarily the shell that is running at the movement.
   ```
   $ echo $SHELL
   ```
2. To change the shell for bob from **`Bash`** to **`Bourne Shell`**
   ```
   $ chsh -s /bin/sh bob
   ```
3. What is the value of the environment variable **`TERM`**
   ```
   echo $TERM
   ```  
4. User profile scripts,  such as **`~/.profile, ~/.bash_profile, ~/.bashrc,`** and others, are executed when a user logs in, allowing the setup of the environment according to personal preferences.  To make changes persistent in Unix-like operating systems, variables, aliases, and other configurations can be added to these profile files.  For example, to add a variable using the command line:
```
echo 'export MY_VARIABLE="example_value"' >> ~/.profile
```
This command appends the export statement to the end of the ~/.profile file, making the variable MY_VARIABLE persistent across sessions.  
To add an alias, like `ll` for `ls -l,` use:
```
echo 'alias ll="ls -l"' >> ~/.profile
```
   Create a new environment variable called **`PROJECT=MERCURY`** and make it persistent by adding the variable to the **`~/.profile`** file.
   ```
   echo export PROJECT=MERCURY >> ~/.profile
   ```
6. Which of the following directories is not part of the PATH variable? <br> inspect the PATH variable to see all the directories found in it with `echo $PATH`
   ```
   /opt/caleston-code
   ```
8. Set an alias called **`up`** for the command **`uptime`** and make it persistent by adding to **`~/.profile`** file.
   ```
   echo alias up=uptime >> ~/.profile
   ```
9. Update Bob's prompt so that it displays the date as per the format below:
Example: **`[Wed Apr 22]bob@caleston-lp10:~$`**
Make sure the change is made persistent.
   ```
   PS1='[\d]\u@\h:\w\$'
   or
   echo 'PS1=[\d]\u@\h:\w$' >> ~/.profile
   ```

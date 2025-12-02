
1. Which command is used to list all the cronjobs created for a user?
```
Run: crontab --help
```
2. How many cronjobs are currently scheduled for bob?
```
Run: crontab -l and count the number of cronjobs (ignore lines starting with # (they are comments)
```
3. How about now? How many cronjobs are scheduled for the root user ?

`sudo : sudo crontab -l`

4. Inspect the cronjobs scheduled for bob again. Which command/script is run at 11 minutes past 11 PM every Tuesday?

```

```

5. Schedule a cronjob to run the script /usr/local/bin/last-reboot.sh on the first day of every month at 6 AM. <br> The script should not run any other day.

```
Use: Run crontab -e. This will open the crontab in the VI Editor. Add the below line to the file:
0 6 1 * * /usr/local/bin/last-reboot.sh
```
6. When will the script /usr/local/bin/system-troubleshooter.sh be run? <br> Inspect the cronjobs scheduled for bob.

```
The first column is 11 = 11th minute

The second column is 23 = 11 PM

The third column is * = every day in a month (1st to the last day of the month)

The fourth column is 2 = only the month of February

The fifth column is * = every day if the week (Monday to Sunday)

This means the script will run at 11 minutes past 11 PM on all days in the month of February
```

7. The script /usr/local/bin/system-debugger.sh was incorrectly scheduled. It should run every half hour at minute 0 and minute 30

Example: 09:00, 09:30, 10:00, 10:30, 11:00, 11:30……so on every half hour.

```
Use Step values for the minute column = */30 OR

Specify the minute column as 00,30 both of which mean at minute zero then minute 30.
To sum up, add this to the crontab:
*/30 * * * * /usr/local/bin/system-debugger.sh
```




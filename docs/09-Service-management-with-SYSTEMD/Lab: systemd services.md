
1. This lab requires several commands to be run as the root user. Always use sudo. <br> Bob's default password is caleston123

2. What is the status of the sample.service unit?

```
Run: sudo systemctl status sample.service
```
3. Try starting the service <br> does it start?

4. Why did the service start fail?

```
Run: sudo journalctl -u sample.service
```
5. Update the [`Service`] section

Set the `ExecStart` to run the script `/bin/bash /root/sample_script.sh`.
Once done, start the service.

```
Run: sudo vi /etc/systemd/system/sample.service
Add /bin/bash /root/sample_script.sh to ExecStart
Save and Exit.
and then start the service: - sudo systemctl start sample.service
```
6. Inspect the status of the service now. <br> What is the status?

7. nable this service now so that it will be started automatically after a reboot for multi-user.target

```
Run: sudo systemctl enable sample.service
```
8. Now update the service to ensure that it restarts when stopped for any reason. <br> Use the Restart=always derivative.
```
Run: sudo vi /etc/systemd/system/sample.service
Add Restart=always to the Service section.
Save and Exit
```
9. Try and restart the service now. <br> there seems to be a warning what is the fix

```
sudo systemctl start sample.service or restart will fail.
Since you updated the service unit file, you need to reload it first.
```
10. Reload the service unit file

```
Run: sudo systemctl daemon-reload
```
11. 

12. 








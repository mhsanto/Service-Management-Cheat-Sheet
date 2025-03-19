# Service-Management-Cheat-Sheet
This cheat sheet provides a quick reference guide for managing both system and user services on a Linux system using systemd. It covers common tasks such as starting, stopping, enabling, and disabling services, as well as creating new services based on existing ones.


---

## System Services

### Location
- System services are located in `/etc/systemd/system/`.
- Example services:
  - `exampleapp.service`
  - `datahandler.service`

### Service File
- These service files are entry points to the binary.

### Managing System Services
1. **Log in as Root**
   - To avoid password prompts, log in as the root user:
     ```sh
     sudo -i
     ```

2. **Create a New Service (Copy Existing)**
   - Copy an existing service file to create a new one:
     ```sh
     cp /etc/systemd/system/exampleapp.service /etc/systemd/system/newapp.service
     ```

3. **Check Service Status**
   - Check the status of a service:
     ```sh
     systemctl status newapp.service
     ```

4. **Start a Service**
   - Start the service:
     ```sh
     systemctl start newapp.service
     ```

5. **Stop a Service**
   - Stop the service:
     ```sh
     systemctl stop newapp.service
     ```

6. **Enable/Disable a Service on Startup**
   - Enable the service to run on startup:
     ```sh
     systemctl enable newapp.service
     ```
   - Disable the service so it doesn’t run on startup:
     ```sh
     systemctl disable newapp.service
     ```

7. **Remove a Service**
   - After disabling, stop the service and remove the service file if necessary:
     ```sh
     systemctl stop newapp.service
     rm /etc/systemd/system/newapp.service
     ```

## User Services

### Location
- User services are located in `/etc/systemd/user/`.
- Typically used for apps with a UI that need to run as the active user (logged into the desktop manager).
- Example service: `trendboard.service`

### Managing User Services
1. **Log in as the User**
   - Ensure you’re logged in as the correct user:
     ```sh
     su - [username]
     ```

2. **Check Service Status**
   - Check the status of a user service:
     ```sh
     systemctl --user status usermanager.service
     ```

3. **Stop/Restart a Service**
   - Stop the service:
     ```sh
     systemctl --user stop usermanager.service
     ```
   - Restart the service:
     ```sh
     systemctl --user restart usermanager.service
     ```

4. **Enable/Disable a Service on Startup**
   - Enable the user service to run on startup:
     ```sh
     systemctl --user enable usermanager.service
     ```
   - Disable the user service so it doesn’t run on startup:
     ```sh
     systemctl --user disable usermanager.service
     ```

5. **Remove a User Service**
   - After disabling, stop the service and remove the service file if necessary:
     ```sh
     systemctl --user stop usermanager.service
     rm /etc/systemd/user/usermanager.service

     ```
6. **View User Service Logs**
   - View and follow the logs for a user service (while logged in as the user that runs the service):
   ```sh
   journalctl --user -fu serviceName.service
   ```
### Additional Notes
- Restart, stop, or start these services through the UI if applicable.
- Check the uptime after restarting to ensure it has restarted successfully.


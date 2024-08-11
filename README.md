# Service-Management-Cheat-Sheet
This cheat sheet provides a quick reference guide for managing both system and user services on a Linux system using systemd. It covers common tasks such as starting, stopping, enabling, and disabling services, as well as creating new services based on existing ones.
Here’s a cheat sheet based on the information your senior developer provided. You can format it and upload it to GitHub as needed.

---

Here's the updated cheat sheet with the additional information on deploying your Go application:

---

# Service Management Cheat Sheet

## System Services

### Location
- System services are located in `/etc/systemd/system/`.
- Example services:
  - `angelshoe.service`
  - `collector.service`

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
     cp /etc/systemd/system/collector.service /etc/systemd/system/santossystem.service
     ```

3. **Check Service Status**
   - Check the status of a service:
     ```sh
     systemctl status santossystem
     ```

4. **Start a Service**
   - Start the service:
     ```sh
     service santossystem start
     ```

5. **Stop a Service**
   - Stop the service:
     ```sh
     service santossystem stop
     ```

6. **Enable/Disable a Service on Startup**
   - Enable the service to run on startup:
     ```sh
     systemctl enable santossystem.service
     ```
   - Disable the service so it doesn’t run on startup:
     ```sh
     systemctl disable santossystem.service
     ```

7. **Remove a Service**
   - After disabling, stop the service and remove the service file if necessary:
     ```sh
     systemctl stop santossystem.service
     rm /etc/systemd/system/santossystem.service
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
     systemctl --user status trendboard.service
     ```

3. **Stop/Restart a Service**
   - Stop the service:
     ```sh
     systemctl --user stop trendboard.service
     ```
   - Restart the service:
     ```sh
     systemctl --user restart trendboard.service
     ```

4. **Enable/Disable a Service on Startup**
   - Enable the user service to run on startup:
     ```sh
     systemctl --user enable trendboard.service
     ```
   - Disable the user service so it doesn’t run on startup:
     ```sh
     systemctl --user disable trendboard.service
     ```

5. **Remove a User Service**
   - After disabling, stop the service and remove the service file if necessary:
     ```sh
     systemctl --user stop trendboard.service
     rm /etc/systemd/user/trendboard.service
     ```

### Additional Notes
- Restart, stop, or start these services through the UI if applicable.
- Check the uptime after restarting to ensure it has restarted successfully.

## Deploying Your Go Application

1. **Navigate to the Project Directory**
   - Change to your Go project’s directory:
     ```sh
     cd /bundle/remote
     ```

2. **Build the Application**
   - Compile your Go code into a binary executable:
     ```sh
     go build
     ```
   - This creates a binary named `remote`.

3. **Transfer the Binary to the Target Machine**
   - Securely copy the binary to the target machine:
     ```sh
     scp remote idx@[IP_ADDRESS]:~/remote
     ```
   - Replace `[IP_ADDRESS]` with the actual IP address of your target machine.

4. **SSH into the Target Machine**
   - Log in to the target machine as the `idx` user:
     ```sh
     ssh idx@[IP_ADDRESS]
     ```

5. **Run the Application**
   - Execute the application on the target machine:
     ```sh
     sudo ./remote -port=7686
     ```
   - Use `sudo` if elevated privileges are required to restart services.

6. **Alternative: Create a System Service**
   - Instead of running the application manually, consider creating a system service to manage it, allowing for better control and automatic management.

---


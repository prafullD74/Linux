# [Manage Systemd Services with systemctl on Linux](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)

### Service Management

>The fundamental purpose of an init system is to initialize the components that must be started after the Linux kernel is booted.  The init system is also used to manage services and daemons for the server at any point while the system is running.

In `systemd`, the target of most actions are “units”, which are resources that `systemd` knows how to manage. Units are categorized by the type of resource they represent and they are defined with files known as unit files. The type of each unit can be inferred from the suffix on the end of the file.

### What is systemctl used for in Linux?
>`systemctl` is a command-line utility used to manage and interact with the systemd system and service manager in Linux. It allows you to start, stop, restart, enable, and disable services, as well as check their status.

1. **Starting and Stopping Services**
    ```bash
    sudo systemctl start application.service
    ```
    ```bash
    sudo systemctl start application
    ```
    ```bash
    sudo systemctl stop application.service
    ```
2. **Restarting and Reloading**
    - The `restart` command stops and then starts a service, effectively reloading the service configuration. The `reload` command, on the other hand, reloads the service configuration without stopping the service. This is useful when you’ve made changes to the service configuration files and want to apply those changes without disrupting the service.
    ```bash
    sudo systemctl restart application.service
    ```
    ```bash
    sudo systemctl reload application.service
    ```
    ```bash
    sudo systemctl reload-or-restart application.service
    ```
    - If you are unsure whether the service has the functionality to reload its configuration, you can issue the `reload-or-restart` command. This will reload the configuration in-place if available. Otherwise, it will restart the service so the new configuration is picked up.

3. **Enabling and Disabling Services**
    - To start a service at boot, use the `enable` command. This will create a symbolic link from the system’s copy of the service file (usually in /lib/systemd/system or /etc/systemd/system) into the location on disk where systemd looks for autostart files (usually /etc/systemd/system/some_target.target.wants.)
    ```bash
    sudo systemctl enable application.service
    ```
    ```bash
    sudo systemctl disable application.service
    ``` 
    - To disable the service from starting automatically.

4. **Checking the Status of Services**
    ```bash
    systemctl status application.service
    ```
    ```bash
    systemctl is-active application.service
    ``` 
    - To check to see if a unit is currently active (running), you can use the `is-active` command.

    ```bash
    systemctl is-enabled application.service
    ```
    - To see if the unit is enabled.
    ```bash
    systemctl is-failed application.service
    ``` 
    - This will return `active` if it is running properly or `failed` if an error occurred. If the unit was intentionally stopped, it may return unknown or inactive. An exit status of “0” indicates that a failure occurred and an exit status of “1” indicates any other status.

### System State Overview

1. **Listing Current Units**
    ```bash
    systemctl list-units
    ``` 
    - To see a list of all of the active units.
    - Since the `list-units` command shows only active units by default, all of the entries above will show `loaded` in the LOAD column and `active` in the ACTIVE column. This display is actually the default behavior of `systemctl` when called without additional commands, so you will see the same thing if you call `systemctl` with no arguments.
    ```bash
    systemctl list-units --all
    ``` 
    - To see all of the units that systemd has loaded (or attempted to load), regardless of whether they are currently active.
    ```bash
    systemctl list-units --all --state=inactive
    ``` 
    - we can use the `--state=` flag to indicate the LOAD, ACTIVE, or SUB states that we wish to see
    ```bash
    systemctl list-units --type=
    ```
2. **Listing All Unit Files**
    ```bash
    systemctl list-unit-files
    ```
    - To see every available unit file within the systemd paths, including those that systemd has not attempted to load.
    - The state will usually be enabled, disabled, static, or masked. In this context, static means that the unit file does not contain an install section, which is used to enable a unit.

### Unit Management

1. **Editing Unit Files**
    ```bash
    sudo systemctl edit nginx.service
    ``` 
    - This will be a blank file that can be used to override or add directives to the unit definition. A directory will be created within the `/etc/systemd/system` directory which contains the name of the unit with `.d` appended. For instance, for the `nginx.service`, a directory called `nginx.service.d` will be created. Within this directory, a snippet will be created called `override.conf`. When the unit is loaded, `systemd` will, in memory, merge the override snippet with the full unit file. The snippet’s directives will take precedence over those found in the original unit file
    ```bash
    sudo systemctl edit --full nginx.service
    ``` 
    - If you wish to edit the full unit file instead of creating a snippet, you can pass the `--full` flag.
    ```bash
    sudo rm -r /etc/systemd/system/nginx.service.d
    ``` 
    - To remove any additions you have made, either delete the unit’s `.d` configuration directory or the modified service file from `/etc/systemd/system`.
    ```bash
    sudo rm /etc/systemd/system/nginx.service
    ``` 
    - To remove a full modified unit file.
2. **Displaying a Unit File**
    ```bash
    systemctl cat atd.service
    ```
3. **Displaying Dependencies**
    - This will display a hierarchy mapping the dependencies that must be dealt with in order to start the unit in question
    - `--all` flag to recursively list all dependencies.
    - `--reverse` flag to show reverse dependencies
    - `-before` and `--after` flags, which can be used to show units that depend on the specified unit starting before and after themselves, respectively.
    ```bash
    systemctl list-dependencies sshd.service
    ```
4. **Checking Unit Properties**
    - This will display a list of properties that are set for the specified unit using a key=value format.
    ```bash
    systemctl show sshd.service
    ```
    ```bash
    systemctl show sshd.service -p Conflicts
    ```
    - `-p` flag to display a single property.
5. **Masking and Unmasking Units**
    - `systemd` also has the ability to mark a unit as completely unstartable, automatically or manually, by linking it to `/dev/null`. This is called masking the unit, and is possible with the `mask` command.
    ```bash
    sudo systemctl mask nginx.service
    ```
    - Use below command to verify service is now listed as masked
    ```bash
    systemctl list-unit-files
    ```
    - To unmask a unit, making it available for use again, use the `unmask` command.
    ```bash
    sudo systemctl unmask nginx.service
    ```
### Adjusting the System State (Runlevel) with Targets

>Targets are special unit files that describe a system state or synchronization point. Like other units, the files that define targets can be identified by their suffix, which in this case is`.target`. Targets do not do much themselves, but are instead used to group other units together.

1. **Getting and Setting the Default Target**
    ```bash
    systemctl get-default
    ```
    - The `systemd` process has a default target that it uses when booting the system. Satisfying the cascade of dependencies from that single target will bring the system into the desired state.
    ```bash
    sudo systemctl set-default graphical.target
    ```
    - If you wish to set a different default target, you can use the `set-default`.
2. **Listing Available Targets**
    ```bash
    systemctl list-unit-files --type=target
    ```
    - To see all of the active targets
    ```bash
    systemctl list-units --type=target
    ```
3. **Isolating Targets**
    - It is possible to start all of the units associated with a target and stop all units that are not part of the dependency tree.
    - For instance, if you are operating in a graphical environment with `graphical.target` active, you can shut down the graphical system and put the system into a multi-user command line state by isolating the `multi-user.target`. Since `graphical.target` depends on `multi-user.target` but not the other way around, all of the graphical units will be stopped.
    ```bash
    systemctl list-dependencies multi-user.target
    ```
    - Take a look at the dependencies of the target you are isolating before performing this procedure to ensure that you are not stopping vital services.
    - When you are satisfied with the units that will be kept alive, you can isolate the target.
    ```bash
    sudo systemctl isolate multi-user.target
    ```
4. **Using Shortcuts for Important Events**
    - There are targets defined for important events like powering off or rebooting.
    - To put the system into rescue (single-user) mode, you can use the `rescue` command.
    ```bash
    sudo systemctl rescue
    ```
    - `halt` command is used to stop all CPU functions and typically prepares the system for shutdown
    ```bash
    sudo systemctl halt
    ```
    - To initiate a full shutdown
    ```bash
    sudo systemctl poweroff
    ```
    ```bash
    sudo systemctl reboot
    ```
    - To reboot the system
    ```bash
    sudo reboot
    ```
### Reloading Configuration without Full Restart
- To reload the configuration of a service without restarting it, use the reload command followed by the service name.
    ```bash
    sudo systemctl reload httpd
    ```
### Common Errors and Debugging
1. **“Failed to start unit” or “Unit not found” errors**
    - Ensure the service file is located in the correct directory, such as `/etc/systemd/system/` or `/lib/systemd/system/`, and that it has the correct file name and extension (e.g., `httpd.service`).
    ```bash
    sudo systemctl cat httpd
    ```
    - Will display the service file contents, allowing you to inspect the file for syntax errors or incorrect dependencies.
    - For system services, configuration files should be placed in `/lib/systemd/system/`, while custom services or overrides should be placed in `/etc/systemd/system/`. This distinction is important to ensure that custom configurations take precedence over system defaults.
2. **Permissions issues (e.g., needing sudo)**
    - Ensure you are running the `systemctl` commands with the necessary permissions, typically by prefixing them with `sudo`. 
3. **Misplaced or invalid unit files**
    - If you have created custom unit files, ensure they are correctly named and follow the expected syntax.
    - To verify the unit file location and format, use the following commands:
    ```bash
    sudo systemctl list-unit-files
    sudo systemctl cat <service_name>
    ```




# [Journalctl](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs)
>The system that collects and manages these logs is known as the journal. The journal is implemented with the journald daemon, which handles all of the messages produced by the kernel, initrd, services, etc

- The `journald` daemon collects data from all available sources and stores them in a binary format for easy and dynamic manipulation.
- Storing the log data in a binary format also means that the data can be displayed in arbitrary output formats depending on what you need at the moment.

### Setting the System Time
1. By default, `systemd` will display results in local time. The `systemd` suite actually comes with a tool called `timedatectl` that can help to make sure the timezone is set up correctly.
    - To list the timezones available on your system.
    ```bash
    timedatectl list-timezones
    ```
    ```bash
    sudo timedatectl set-timezone zone
    ```
    ```bash
    timedatectl status
    ```
### Basic Log Viewing
- To see the logs that the `journald` daemon has collected, use the ``journalctl` command. `--utc` flag to display the timestamps in UTC.
    ```bash
    journalctl --utc
    ```
### Journal Filtering by Time
1. **Displaying Logs from the Current Boot**
    - `-b` flag will show you all of the journal entries that have been collected since the most recent reboot.
    ```bash
    journalctl -b
    ```
2. **Past Boots**
    - The journal can save information from many previous boots. Some distributions enable saving previous boot information by default, while others disable this feature. 
    - To enable persistent boot information, you can either create the directory to store the journal.
    ```bash
    sudo mkdir -p /var/log/journal
    ```
    ```bash
    sudo nano /etc/systemd/journald.conf
    ```
    - Edit the journal configuration file, Under the `[Journal]` section, set the `Storage=` option to “persistent” to enable persistent logging.
    ```bash
    journalctl --list-boots
    ```
    - `--list-boots` option to see the boots that `journald` knows about.
    - To see the journal from the previous boot, use the `-1` relative pointer with the `-b` flag or use the boot ID to call back the data from a boot.
    ```bash
    journalctl -b -1
    journalctl -b caf0524a1d394ce0bdbcff75b94444fe
    ```
3. **Time Windows**
    - Can filter by arbitrary time limits using the `--since` and `--until` options, which restrict the entries displayed to those after or before the given time, respectively.
    - For absolute time values, you should use the following format: `YYYY-MM-DD HH:MM:SS`
    ```bash
    journalctl --since "2015-01-10 17:15:00"
    ```
    ```bash
    journalctl --since "2015-01-10" --until "2015-01-11 03:00"
    ```
    - Use the words “yesterday”, “today”, “tomorrow”, or “now”
    ```bash
    journalctl --since yesterday
    ```
    - Use  relative times by prepending “-” or “+” to a numbered value or using words like “ago” in a sentence construction. If you received reports of a service interruption starting at 9:00 AM and continuing until an hour ago.
    ```bash
    journalctl --since 09:00 --until "1 hour ago"
    ```
### Filtering by Message Interest
>how to filter based on what service or component you are interested in.
1. **By Unit**
    - Most useful way of filtering is by the unit you are interested in. We can use the`-u` option to filter. Ex. to see all of the logs from an Nginx unit on our system
    ```bash
    journalctl -u nginx.service
    ```
    - To filter by time as well in order to display the lines you are interested in.
    ```bash
    journalctl -u nginx.service --since today
    ```
    - Example, For instance, if your Nginx process is connected to a PHP-FPM unit to process dynamic content, you can merge the entries from both in chronological order by specifying both units.
    ```bash
    journalctl -u nginx.service -u php-fpm.service --since today
    ```
2. **By Process, User, or Group ID**
    - Many services create smaller tasks, called child processes, to get work done. If you know the exact ID (PID) of the process you're looking for, you can narrow your search by using its `-pid`.
    ```bash
    journalctl _PID=8088
    ```
    - With `_UID` or `_GID` filters, use to show all of the entries logged from a specific user or group. Use the ID that was returned. Example "UID=33"
    ```bash
    id -u www-data
    ```
    ```bash
    journalctl _UID=33 --since today
    ```
    - To find out about all of the available journal fields.
    ```bash
    man systemd.journal-fields
    ```
    - The `-F` option can be used to show all of the available values for a given journal field
    ```bash
    journalctl -F _GID
    ```
3. **By Component Path**
    - We can also filter by providing a path location. If the path leads to an executable, journalctl will display all of the entries that involve the executable in .
    ```bash
    journalctl /usr/bin/bash
    ```
4. **Displaying Kernel Messages**
    - Using `-k` or `--dmesg` flags, Kernel messages, those usually found in `dmesg` output, can be retrieved from the journal as well.
    ```bash
    journalctl -k
    ```
    ```bash
    journalctl -k -b -5
    ```
5. **By Priority**
    - One filter that system administrators often are interested in is the message priority. Use `journalctl` to display only messages of a specified priority or above by using the `-p` option. This allows you to filter out lower priority messages.
    ```bash
    journalctl -p err -b
    ```
    - use either the priority name or its corresponding numeric value. In order of highest to lowest priority, these are:
        - 0: emerg
        - 1: alert
        - 2: crit
        - 3: err
        - 4: warning
        - 5: notice
        - 6: info
        - 7: debug

### Modifying the Journal Display





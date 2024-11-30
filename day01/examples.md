### **Day 1 - Content Files**

## SSH Tools
### Download Links:
- **PuTTY:** [Download PuTTY](https://www.putty.org/)
- **Super PuTTY:** [Download Super PuTTY](https://github.com/jimradford/superputty/releases)
- **MobaXterm:** [Download MobaXterm](https://mobaxterm.mobatek.net/download.html)
- **Git Bash:** [Download Git Bash](https://gitforwindows.org/)

## FTP Tools
### Download Links:
- **WinSCP:** [Download WinSCP](https://winscp.net/eng/download.php) (Windows)
- **FileZilla:** [Download FileZilla](https://filezilla-project.org/download.php) (Cross-platform)

## Linux Overview:
- **Open Source:** Linux is an open-source operating system, freely available for use and modification.
- **Case Sensitivity:** Linux commands and file names are case-sensitive.

## Popular Linux Distributions:
1. **RedHat**: Enterprise-focused, subscription-based.
2. **CentOS**: Free, community version of RedHat.
3. **Ubuntu**: User-friendly, widely used for desktops and servers.
4. **SUSE Linux**: Known for enterprise reliability.
5. **Fedora**: Cutting-edge features, backed by RedHat.
6. **Gentoo**: Highly customizable, source-based.
7. **Mandriva**: User-friendly with a strong community focus.
8. **Debian**: Stable and versatile, foundation for Ubuntu.
9. **Slackware**: One of the oldest distributions, minimalistic.

## Linux Directory Structure Examples:
- **Windows Path Example:** `C:\users`
- **Linux Path Example:** `/home` (Contains user directories)

### Important Directories:
- **`/bin`**: Contains binary files for essential commands like `ls`, `mkdir`, and `cp`.
  ```bash
  ls /bin
  ```

- **`/sbin`**: Contains system binaries, accessible only by the root user.
  ```bash
  ls /sbin
  ```

- **`/etc`**: Stores system configuration files.
  - Important files:
    - `sudoers`: Configures sudo privileges.
    - `passwd`: Stores user account information.
    - `shadow`: Stores encrypted passwords.
    - `group`: Contains group information.
    - `motd`: Message displayed after login.

  ```bash
  cat /etc/passwd
  ```

- **`/opt`**: Directory for third-party software installations (e.g., Jenkins, SonarQube).
  ```bash
  ls /opt
  ```

- **`/lib`**: Contains shared libraries needed for system binaries.
  ```bash
  ls /lib
  ```

- **`/dev`**: Contains device files representing hardware (e.g., `sda1` for hard disks).
  ```bash
  ls /dev
  ```

- **`/proc`**: Provides information about system processes and hardware.
  ```bash
  cat /proc/cpuinfo
  ```

- **`/var`**: Contains log files and other variable data.
  ```bash
  ls /var/log
  ```

- **`/tmp`**: Temporary files; accessible to all users.
  ```bash
  cd /tmp
  ```

## User Types:
1. **Super User/Root:** Has full system privileges (root user).
2. **Normal Users:** Regular users with limited permissions.
3. **System Users:** Automatically created when installing software (e.g., `www-data` for web servers).

## Basic Commands Examples:
- **Create a directory:** 
  ```bash
  mkdir my_directory
  ```

- **List files in a directory:** 
  ```bash
  ls
  ls -la  # Detailed list with hidden files
  ```

- **Check the current directory:** 
  ```bash
  pwd
  ```

- **Change directories:** 
  ```bash
  cd /path/to/directory
  cd ..  # Go up one level
  ```

- **Remove a directory:** 
  ```bash
  rmdir empty_directory  # Only works if the directory is empty
  ```

- **Remove files or directories:** 
  ```bash
  rm file_name
  rm -r directory_name  # Remove directory and contents
  ```

- **Display directory structure in a tree format (if `tree` is installed):**
  ```bash
  tree /path/to/directory
  ```
```

---

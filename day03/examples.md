
# Day 3 : Permissions and Ownership

## File and Directory Creation Examples
1. **Create a new file:**
   ```bash
   touch myfile.txt
   ```
   Creates an empty file named `myfile.txt`.

2. **Create a file inside a specific directory without navigating to it:**
   ```bash
   touch devops/test.txt
   ```
   This command creates `test.txt` inside the `devops` directory directly.

3. **Display the contents of a directory without entering it:**
   ```bash
   ls /devops
   ```
   Lists the contents of the `/devops` directory.

4. **Find empty files in the current directory and subdirectories:**
   ```bash
   find . -type f -empty
   ```
   Useful for identifying files that need content or cleanup.

5. **Find empty directories:**
   ```bash
   find . -type d -empty
   ```
   Helps locate unused directories.

6. **Find a file with case-insensitive matching:**
   ```bash
   find . -iname "kalandar.sh"
   ```
   Finds `kalandar.sh`, ignoring case differences.

7. **Find all hidden files:**
   ```bash
   find . -type f -name ".*"
   ```
   Searches for all hidden files in the current directory and subdirectories.

---

## Understanding Permissions
- **Default file and directory permissions:**
  - For a normal user:
    - File: `0666` (read and write for everyone, minus the `umask`).
    - Directory: `0775` (full access for owner and group, read and execute for others).
  - For the root user:
    - File: `0666` minus `umask` (default `0644`).
    - Directory: `0777` minus `umask` (default `0755`).

---

## Real-Life Scenarios
1. **Restricting Access to Sensitive Files:**
   - Change file permissions to allow only the owner access:
     ```bash
     chmod 600 secrets.txt
     ```
     Useful for storing sensitive data such as API keys.

2. **Granting Group Access for Collaboration:**
   - Allow a specific group to read and write to a project directory:
     ```bash
     chmod -R 770 project_directory
     ```
     Ensures that only the owner and group members can modify files.

3. **Updating Permissions Recursively for a Directory:**
   - Update permissions for all files and subdirectories:
     ```bash
     chmod -R 755 website_files
     ```
     Commonly used when deploying web projects.

---

## Changing umask
1. **Temporary Session:**
   ```bash
   umask 0022
   ```
   Changes the umask value for the current session only.

2. **Permanent Change for All Users:**
   - Edit the `/etc/profile` file to modify the default umask:
     ```bash
     sudo vi /etc/profile
     ```
     Add or update the line:
     ```bash
     umask 0022
     ```

---

## Using `chmod` with Numeric Permissions
1. **Set read-only permissions for all users:**
   ```bash
   chmod 444 myfile.txt
   ```
   Everyone can read, but no one can modify.

2. **Grant execute permissions to the owner:**
   ```bash
   chmod 700 script.sh
   ```
   Only the owner can read, write, and execute.

3. **Recursively update permissions:**
   ```bash
   chmod -R 755 /var/www/html
   ```
   Useful for web servers where files need specific permissions.
```
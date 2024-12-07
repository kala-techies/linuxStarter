# Day 3 Commands: Permissions and Ownership

## File and Directory Creation
- **Create an empty file:**
  ```bash
  touch filename
  ```

- **Create a file inside a specific directory:**
  ```bash
  touch directory_name/filename
  ```

- **List the contents of a directory without navigating:**
  ```bash
  ls /directory_name
  ```

## Finding Files and Directories
- **Find empty files:**
  ```bash
  find . -type f -empty
  ```

- **Find empty directories:**
  ```bash
  find . -type d -empty
  ```

- **Find a file (case-insensitive):**
  ```bash
  find . -iname filename
  ```

- **Find all hidden files:**
  ```bash
  find . -type f -name ".*"
  ```

## Viewing and Changing Permissions
- **View the current umask:**
  ```bash
  umask
  ```

- **Change umask for the current session:**
  ```bash
  umask new_value
  ```

- **Change umask permanently:**
  - Edit the `/etc/profile` file:
    ```bash
    sudo vi /etc/profile
    ```
    Add or update:
    ```bash
    umask new_value
    ```

- **Change file permissions with `chmod`:**
  - Grant read-only access to all users:
    ```bash
    chmod 444 filename
    ```

  - Allow full access to the owner:
    ```bash
    chmod 700 filename
    ```

  - Recursively change permissions for a directory:
    ```bash
    chmod -R 755 directory_name
    ```

## Real-Life Use Cases
- **Restrict access to sensitive files:**
  ```bash
  chmod 600 secrets.txt
  ```

- **Grant group access for collaboration:**
  ```bash
  chmod -R 770 shared_folder
  ```

- **Set execute permissions for scripts:**
  ```bash
  chmod +x script.sh
  ```
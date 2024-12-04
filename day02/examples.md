# Day 2 Navigating the Filesystem and File Operations

### Creating Directories:
- **Create a simple directory:**
  ```bash
  mkdir my_folder
  ```
  This command creates a new directory called `my_folder`.

- **Create a directory with verbose output:**
  ```bash
  mkdir -v my_folder
  ```
  This provides a confirmation message indicating the directory creation.

- **Create nested directories with parent structure:**
  ```bash
  mkdir -p kalandar/shaik/dada/test
  ```
  The `-p` option ensures all parent directories are created if they don’t exist.

- **Create a directory with specific permissions:**
  ```bash
  mkdir -m 700 secure_folder
  ```
  This creates `secure_folder` with permissions `700` (only the owner can read, write, and execute).

### Listing Files and Directories:
- **List files and directories:**
  ```bash
  ls
  ```
  Lists the contents of the current directory.

- **List files in long format (detailed information):**
  ```bash
  ls -l
  ```
  Provides detailed information including permissions, owner, size, and modification date.

- **List files sorted by creation time (newest first):**
  ```bash
  ls -lt
  ```
  Sorts files by modification time, showing the newest files first.

- **List files in reverse order (oldest first):**
  ```bash
  ls -ltr
  ```
  Displays files in reverse order, showing the oldest files first.

- **List all files, including hidden files:**
  ```bash
  ls -a
  ```
  Shows all files, including hidden files (those starting with `.`).

- **List files with human-readable sizes:**
  ```bash
  ls -lh
  ```
  Displays file sizes in human-readable format (e.g., KB, MB).

- **View inode numbers of files:**
  ```bash
  ls -i
  ```
  Each file is associated with an inode (index node) number that contains metadata.

### Viewing Directory Structure:
- **View the directory tree structure:**
  ```bash
  tree
  ```
  Displays the folder structure in a tree format. Requires installation:
  ```bash
  sudo apt install tree  # For Debian-based systems
  ```

### Navigating Directories:
- **Print the current working directory:**
  ```bash
  pwd
  ```
  Shows the full path of the current directory.

- **Change to the home directory:**
  ```bash
  cd ~
  ```
  Navigates to the user’s home directory.

- **Return to the previous directory:**
  ```bash
  cd -
  ```
  Switches back to the previous working directory.

### Removing Directories and Files:
- **Remove an empty directory:**
  ```bash
  rmdir empty_folder
  ```
  Only works if the directory is empty.

- **Remove a directory and its contents recursively:**
  ```bash
  rm -rf my_folder
  ```
  Deletes the directory and all its contents without prompting.

- **Force remove a file without confirmation:**
  ```bash
  rm -f myfile.txt
  ```
  Removes a file forcefully without asking for confirmation.

### Accessing Manual Pages:
- **View the manual page for a command:**
  ```bash
  man ls
  ```
  Displays the manual for the `ls` command, explaining its usage and options.

---

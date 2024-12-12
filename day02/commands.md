# Day 2 Commands: Filesystem Navigation and File Operations

## Directory Management
- **Create a directory:**
  ```bash
  mkdir directory_name
  ```

- **Create a directory with verbose output:**
  ```bash
  mkdir -v directory_name
  ```

- **Create nested directories (parent directories):**
  ```bash
  mkdir -p parent_directory/sub_directory/sub_sub_directory
  ```

- **Create a directory with specific permissions:**
  ```bash
  mkdir -m 700 secure_directory
  ```

## Listing Files and Directories
- **List files in the current directory:**
  ```bash
  ls
  ```

- **List files with detailed information (long list):**
  ```bash
  ls -l
  ```

- **List files sorted by modification time:**
  ```bash
  ls -lt
  ```

- **List files in reverse time order:**
  ```bash
  ls -ltr
  ```

- **List all files, including hidden ones:**
  ```bash
  ls -a
  ```

- **List files in human-readable format (sizes in KB, MB, etc.):**
  ```bash
  ls -lh
  ```

- **Display inode numbers for files:**
  ```bash
  ls -i
  ```

## Navigation Commands
- **Print the current directory path:**
  ```bash
  pwd
  ```

- **Navigate to the home directory:**
  ```bash
  cd ~
  ```

- **Navigate to the previous directory:**
  ```bash
  cd -
  ```

- **Navigate to a specific directory:**
  ```bash
  cd /path/to/directory
  ```

## Directory and File Removal
- **Remove an empty directory:**
  ```bash
  rmdir directory_name
  ```

- **Remove a directory and its contents recursively:**
  ```bash
  rm -rf directory_name
  ```

- **Force remove files only:**
  ```bash
  rm -f file_name
  ```

## Viewing Directory Tree
- **Display the directory structure as a tree:**
  ```bash
  tree
  ```
  *(Note: `tree` needs to be installed via `sudo apt install tree` on Ubuntu or similar for other distros.)*

## Using the `man` Command
- **Get the manual for a command:**
  ```bash
  man command_name
  ```
  Example:
  ```bash
  man ls
  ```

## Real-Life Use Cases
- **Create a project structure with multiple subfolders:**
  ```bash
  mkdir -p project/src project/tests project/docs
  ```

- **List all files, including hidden ones, in a specific directory:**
  ```bash
  ls -a /path/to/directory
  ```

- **View detailed information about files in a directory:**
  ```bash
  ls -lh /path/to/directory
  ```

- **Navigate back to the previous working directory:**
  ```bash
  cd -
  ```

- **Delete a directory along with all its contents:**
  ```bash
  rm -rf old_project
  ```
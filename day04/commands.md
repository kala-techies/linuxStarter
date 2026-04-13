
# Day 2 Commands: Filesystem Navigation and File Operations

## Directory Management
- **Create a directory:**
  ```bash
  mkdir directory_name
  ```

# Day 04 — Filesystem Navigation and File Operations

This file lists common Linux filesystem and navigation commands with a few practical examples and short safety notes.

## Directory management

- Create a directory:
```bash
mkdir directory_name
```

- Create a directory with verbose output:
```bash
mkdir -v directory_name
```

- Create nested directories (parents as needed):
```bash
mkdir -p parent_directory/sub_directory/sub_sub_directory
```

- Create a directory with specific permissions:
```bash
mkdir -m 700 secure_directory
```

## Listing files and directories

- List files in the current directory:
```bash
ls
```

- Long listing (detailed info):
```bash
ls -l
```

- Sort by modification time (newest first):
```bash
ls -lt
```

- Reverse time order (oldest first):
```bash
ls -ltr
```

- Show all files including hidden ones:
```bash
ls -a
```

- Human-readable sizes:
```bash
ls -lh
```

- Show inode numbers:
```bash
ls -i
```

## Navigation commands

- Print current directory:
```bash
pwd
```

- Go to the home directory:
```bash
cd ~
```

- Go to the previous directory:
```bash
cd -
```

- Change to a specific directory:
```bash
cd /path/to/directory
```

## Removing directories and files

- Remove an empty directory:
```bash
rmdir directory_name
```

- Remove a directory and its contents recursively (dangerous):
```bash
rm -rf directory_name
```
Note: rm -rf is destructive. Consider safer alternatives like `rm -rI` (interactive for multiple files) or using a trash utility such as `trash-cli`.

- Force remove a file:
```bash
rm -f file_name
```

## Viewing directory tree

- Display directory structure as a tree:
```bash
tree
```
Note: `tree` may not be installed by default. Install with your distro package manager (for example, Debian/Ubuntu: `sudo apt install tree`; Fedora: `sudo dnf install tree`; Arch: `sudo pacman -S tree`).

## Using the manual (man)

- Show the manual for a command:
```bash
man command_name
```
Example:
```bash
man ls
```

## Real-life examples

- Create a project structure with common subfolders:
```bash
mkdir -p project/src project/tests project/docs
```

- List all files (including hidden) in a specific directory:
```bash
ls -a /path/to/directory
```

- View detailed information for a directory:
```bash
ls -lh /path/to/directory
```

- Navigate back to the previous working directory:
```bash
cd -
```

- Delete an old project directory (use with caution):
```bash
rm -rf old_project
```

## Notes

- This document focuses on common commands; many commands have additional useful options. Use `man` to explore them.
- Be careful with destructive commands (rm, dd, etc.). When in doubt, test on disposable data or use interactive options.

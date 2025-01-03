### **Other Common Linux Commands**

In this section, we will explore common commands used to navigate and manage files and directories, as well as some fundamental commands for general Linux system administration.

---

### **1. Directory Commands**

These commands help you navigate, create, and manage directories in the Linux file system.

#### **1.1. `pwd` - Print Working Directory**

- **Usage:** Displays the current directory you are working in.

  ```bash
  pwd
  ```

  **Example:**

  ```bash
  /home/user/Documents
  ```

#### **1.2. `cd` - Change Directory**

- **Usage:** Allows you to navigate to different directories in the file system.

  **Syntax:**

  ```bash
  cd [directory]
  ```

  **Examples:**

  - `cd /home/user` – Navigate to the `/home/user` directory.
  - `cd ..` – Go to the parent directory (one level up).
  - `cd ~` – Navigate to the home directory.

#### **1.3. `ls` - List Directory Contents**

- **Usage:** Lists the contents of a directory, including files and subdirectories.

  **Syntax:**

  ```bash
  ls [options] [directory]
  ```

  **Examples:**

  - `ls` – List files and directories in the current directory.
  - `ls -l` – List in long format, displaying detailed information (permissions, size, etc.).
  - `ls -a` – List all files, including hidden ones (those starting with a dot).
  - `ls /path/to/directory` – List files in a specific directory.

#### **1.4. `mkdir` - Make Directory**

- **Usage:** Creates a new directory.

  **Syntax:**

  ```bash
  mkdir [directory_name]
  ```

  **Example:**

  ```bash
  mkdir new_folder
  ```

#### **1.5. `rmdir` - Remove Directory**

- **Usage:** Deletes an empty directory.

  **Syntax:**

  ```bash
  rmdir [directory_name]
  ```

  **Example:**

  ```bash
  rmdir old_folder
  ```

#### **1.6. `rm -r` - Remove Directory and Its Contents**

- **Usage:** Deletes a directory and all its contents (files and subdirectories).

  **Syntax:**

  ```bash
  rm -r [directory_name]
  ```

  **Example:**

  ```bash
  rm -r folder_to_delete
  ```

---

### **2. File Commands**

These commands are used for managing files on a Linux system.

#### **2.1. `touch` - Create an Empty File**

- **Usage:** Creates a new empty file or updates the timestamp of an existing file.

  **Syntax:**

  ```bash
  touch [file_name]
  ```

  **Example:**

  ```bash
  touch newfile.txt
  ```

#### **2.2. `cp` - Copy Files or Directories**

- **Usage:** Copies files or directories from one location to another.

  **Syntax:**

  ```bash
  cp [source] [destination]
  ```

  **Examples:**

  - `cp file1.txt file2.txt` – Copies `file1.txt` to `file2.txt` in the same directory.
  - `cp -r dir1/ dir2/` – Copies the contents of `dir1` to `dir2`.

#### **2.3. `mv` - Move or Rename Files/Directories**

- **Usage:** Moves or renames files and directories.

  **Syntax:**

  ```bash
  mv [source] [destination]
  ```

  **Examples:**

  - `mv file1.txt file2.txt` – Renames `file1.txt` to `file2.txt`.
  - `mv file1.txt /home/user/Documents/` – Moves `file1.txt` to the `/home/user/Documents/` directory.

#### **2.4. `rm` - Remove Files or Directories**

- **Usage:** Deletes files or directories.

  **Syntax:**

  ```bash
  rm [file_name]
  ```

  **Examples:**

  - `rm file1.txt` – Deletes `file1.txt`.
  - `rm -r folder_name` – Deletes a directory and all its contents.

#### **2.5. `cat` - Concatenate and Display File Content**

- **Usage:** Displays the content of a file or combines multiple files.

  **Syntax:**

  ```bash
  cat [file_name]
  ```

  **Example:**

  ```bash
  cat myfile.txt
  ```

#### **2.6. `less` - View File Content (with Scrolling)**

- **Usage:** Allows you to view the contents of a file page by page.

  **Syntax:**

  ```bash
  less [file_name]
  ```

  **Example:**

  ```bash
  less myfile.txt
  ```

#### **2.7. `head` - View the Beginning of a File**

- **Usage:** Displays the first few lines of a file.

  **Syntax:**

  ```bash
  head [file_name]
  ```

  **Example:**

  ```bash
  head myfile.txt
  ```

#### **2.8. `tail` - View the End of a File**

- **Usage:** Displays the last few lines of a file.

  **Syntax:**

  ```bash
  tail [file_name]
  ```

  **Example:**

  ```bash
  tail myfile.txt
  ```

---

### **3. File Permissions and Ownership Commands**

These commands allow you to modify file permissions and ownership.

#### **3.1. `chmod` - Change File Permissions**

- **Usage:** Changes the read, write, and execute permissions for files and directories.

  **Syntax:**

  ```bash
  chmod [permissions] [file_name]
  ```

  **Examples:**

  - `chmod +x script.sh` – Grants execute permission to `script.sh`.
  - `chmod 755 file1.txt` – Sets permissions to `rwxr-xr-x` for `file1.txt`.

#### **3.2. `chown` - Change File Ownership**

- **Usage:** Changes the owner and group of a file or directory.

  **Syntax:**

  ```bash
  chown [owner]:[group] [file_name]
  ```

  **Example:**

  ```bash
  chown user1:usergroup myfile.txt
  ```

---

### **4. Other Fundamental and Common Commands**

These are general-purpose commands that help you interact with and manage the Linux system.

#### **4.1. `man` - Display Manual Pages**

- **Usage:** Displays the manual or help page for a command, providing detailed information about how to use it.

  **Syntax:**

  ```bash
  man [command]
  ```

  **Example:**

  ```bash
  man ls
  ```

#### **4.2. `clear` - Clear the Terminal Screen**

- **Usage:** Clears the terminal screen.

  **Syntax:**

  ```bash
  clear
  ```

#### **4.3. `df` - Disk Space Usage**

- **Usage:** Displays the available and used disk space on mounted file systems.

  **Syntax:**

  ```bash
  df
  ```

  **Example:**

  ```bash
  df -h
  ```

#### **4.4. `du` - Disk Usage**

- **Usage:** Shows the disk space used by files and directories.

  **Syntax:**

  ```bash
  du [options] [directory]
  ```

  **Example:**

  ```bash
  du -sh /home/user
  ```

#### **4.5. `top` - Task Manager**

- **Usage:** Displays a dynamic real-time view of the system's processes and resource usage.

  **Syntax:**

  ```bash
  top
  ```

#### **4.6. `ps` - Display Running Processes**

- **Usage:** Displays information about running processes.

  **Syntax:**

  ```bash
  ps
  ```

  **Example:**

  ```bash
  ps aux
  ```

#### **4.7. `kill` - Terminate Processes**

- **Usage:** Terminates a running process by its PID (Process ID).

  **Syntax:**

  ```bash
  kill [PID]
  ```

  **Example:**

  ```bash
  kill 1234
  ```

#### **4.8. `grep` - Search Text in Files**

- **Usage:** Searches for patterns in a file or output from a command.

  **Syntax:**

  ```bash
  grep [pattern] [file]
  ```

  **Example:**

  ```bash
  grep "error" log.txt
  ```

---

### **Conclusion**

These essential Linux commands are the building blocks for interacting with and managing the Linux file system. Whether you are navigating directories, managing files, modifying permissions, or monitoring system performance, mastering these commands is crucial for efficient Linux system management.

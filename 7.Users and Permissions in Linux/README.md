---
# **A Comprehensive Guide to Users and Permissions in Linux**

Linux is a powerful and flexible operating system used in many different environments, from servers to desktop computers. One of its key features is its ability to manage multiple users, each with varying levels of access to files and system resources. Understanding how **users** and **permissions** work is essential for system administrators, developers, and anyone working in a Linux environment. This guide will explain users, groups, and file permissions in detail and in a way that’s easy to understand, even for beginners.
---

### **1. What are Users in Linux?**

In Linux, **users** are individuals or processes that interact with the system. Each user has their own identity and set of privileges. There are different types of users:

- **Root User**: This is the most powerful user in Linux. The root user can do anything on the system, including making changes that could affect the entire system. The root user has **unrestricted access** to all files and commands. Because of its power, it’s important to use the root account carefully to avoid accidental system changes or damage.
- **Regular Users**: These are users who have limited access to the system. Each user can only modify the files they own and is restricted from accessing or modifying other users' files unless given explicit permission. This helps keep the system secure and organized.

#### **Creating and Managing Users**

Linux allows administrators to create, modify, and delete users. Here are some basic commands for managing users:

- **Creating a User**:
  To create a new user, the `useradd` command is used:

  ```bash
  sudo useradd username
  ```

- **Setting a Password for the User**:
  After creating a user, you can assign them a password:

  ```bash
  sudo passwd username
  ```

- **Modifying a User**:
  You can add users to groups or change other properties with the `usermod` command. For example, to add a user to a group:

  ```bash
  sudo usermod -aG groupname username
  ```

- **Deleting a User**:
  To remove a user from the system:
  ```bash
  sudo userdel username
  ```

---

### **2. Understanding Groups in Linux**

A **group** is a collection of users. Groups are used to manage permissions for multiple users efficiently. Instead of giving permission to each user individually, you can assign permissions to a group, and all members of that group will have the same access.

Each user can belong to multiple groups. For instance, a user might belong to both a "staff" group (for general access) and an "admins" group (for administrative tasks).

#### **Creating and Managing Groups**

- **Creating a Group**:
  To create a group, use the `groupadd` command:

  ```bash
  sudo groupadd groupname
  ```

- **Adding a User to a Group**:
  To add a user to a group, use the `usermod` command:

  ```bash
  sudo usermod -aG groupname username
  ```

- **Deleting a Group**:
  To remove a group, use:
  ```bash
  sudo groupdel groupname
  ```

---

### **3. File Permissions in Linux**

One of the most important aspects of Linux is its permission model, which controls how users can access and modify files. Every file in Linux has an **owner** (usually the user who created it), a **group** (a collection of users), and permissions that determine who can read, write, or execute the file.

#### **The Three Types of Permissions**

- **Read (`r`)**: This permission allows a user to open and view the contents of a file. For directories, it allows the user to list the files within the directory.
- **Write (`w`)**: This permission allows a user to modify the contents of a file or add, delete, and rename files within a directory.
- **Execute (`x`)**: This permission allows a user to run a file as a program or script. For directories, it allows the user to **enter** the directory using the `cd` command.

#### **Viewing File Permissions**

To view the permissions of a file or directory, use the `ls -l` command:

```bash
ls -l filename
```

This will output something like:

```
-rwxr-xr--
```

This string has three parts:

1. **File Type** (`-` means a regular file, `d` means a directory).
2. **Owner’s Permissions** (`rwx` means read, write, and execute permissions).
3. **Group’s Permissions** (`r-x` means read and execute permissions, but not write).
4. **Others’ Permissions** (`r--` means read-only for others).

#### **Changing Permissions**

You can change file permissions with the `chmod` command. There are two ways to set permissions: **symbolic mode** and **numeric mode**.

- **Numeric Mode**: Each permission is represented by a number:

  - `r = 4`, `w = 2`, `x = 1`
  - You add these values to set the permissions. For example, `7` (4+2+1) represents `rwx`, `6` (4+2) represents `rw-`, and so on.

  To set permissions using numbers:

  ```bash
  chmod 755 filename  # rwxr-xr-x
  ```

- **Symbolic Mode**: This mode uses letters to represent permissions. You can also add (`+`) or remove (`-`) permissions.

  Example:

  - To give the user execute permission:

    ```bash
    chmod u+x filename
    ```

  - To remove write permission from the group:
    ```bash
    chmod g-w filename
    ```

---

### **4. Special Permissions**

Linux provides some **special permissions** for advanced file access control:

- **Setuid** (`s`): When applied to an executable file, this permission allows the file to be executed with the permissions of the file's owner, not the user who runs it. This is commonly used for programs that need elevated privileges, such as system administration tools.

  Example:

  ```bash
  chmod u+s filename
  ```

- **Setgid** (`s`): This permission applied to a file works similarly to **Setuid**, but for the group. For directories, it ensures that files created within the directory inherit the group of the directory, not the group of the user.

  Example:

  ```bash
  chmod g+s directoryname
  ```

- **Sticky Bit** (`t`): The sticky bit ensures that only the owner of a file can delete or rename it, even if other users have write access to the directory.

  Example:

  ```bash
  chmod +t directoryname
  ```

---

### **5. File Ownership**

Every file and directory in Linux has an **owner** and a **group**. The owner has the ability to change the file, while others may only have read-only or limited access.

#### **Changing File Ownership**

To change the owner or group of a file, use the `chown` command:

- **Changing Owner and Group**:

  ```bash
  sudo chown newuser:newgroup filename
  ```

- **Changing Only the Owner**:

  ```bash
  sudo chown newuser filename
  ```

- **Changing Only the Group**:
  ```bash
  sudo chown :newgroup filename
  ```

---

### **6. Access Control Lists (ACLs)**

In some cases, you might want to provide more **granular control** over file permissions than what the standard owner/group/others model allows. **Access Control Lists (ACLs)** are used for this purpose.

ACLs allow you to assign permissions for individual users and groups, even if they are not the owner or part of the file's group.

To check the ACL of a file, use:

```bash
getfacl filename
```

To set an ACL for a user:

```bash
setfacl -m u:username:rw filename
```

---

### **7. Permissions for Directories**

Directory permissions are similar to file permissions but with one key difference: they control whether a user can **enter** a directory (traverse it) and **list** its contents.

- **Read (`r`)**: Allows listing the contents of the directory.
- **Write (`w`)**: Allows adding, deleting, or renaming files in the directory.
- **Execute (`x`)**: Allows entering the directory (e.g., with the `cd` command).

---

Sure! Let's dive into how to manage permissions in Linux, focusing on the methods for controlling access to files and directories. We'll explore the fundamental tools and commands that you can use to manage permissions effectively.

---

# **How to Manage Permissions in Linux**

Managing permissions is a critical aspect of system security and administration in Linux. It helps determine who can read, modify, or execute files and directories. The Linux permission model is based on three categories: **users**, **groups**, and **others**. Each category can be assigned different levels of access to a file or directory.

---

### **1. Understanding Linux Permissions Model**

The Linux permissions model works on a combination of **read**, **write**, and **execute** permissions, which are granted to **users**, **groups**, and **others**.

#### **Permission Types**:

- **Read (`r`)**: Allows a user to view the content of a file or list the contents of a directory.
- **Write (`w`)**: Allows a user to modify or delete a file or add/remove files in a directory.
- **Execute (`x`)**: Allows a user to run the file as a program or script, or enter a directory (with `cd`).

#### **Permission Categories**:

- **Owner**: The user who owns the file or directory.
- **Group**: A group of users that can be assigned permissions for a file or directory.
- **Others**: All other users who are not the owner or part of the group.

When you look at a file's permissions using `ls -l`, it will show something like:

```
-rwxr-xr--
```

This string breaks down as follows:

- **First Character**: Type of the file (`-` for a regular file, `d` for a directory, `l` for a symbolic link).
- **Next Three Characters**: Permissions for the **owner** (`rwx` = read, write, execute).
- **Next Three Characters**: Permissions for the **group** (`r-x` = read, execute).
- **Last Three Characters**: Permissions for **others** (`r--` = read only).

---

### **2. Viewing Permissions**

To view the permissions of a file or directory, you can use the `ls -l` command. It will display the permissions, ownership, and group details:

```bash
ls -l filename
```

Example output:

```
-rwxr-xr-- 1 user group 1234 Jan 1 12:34 filename
```

This tells you:

- The file is readable, writable, and executable by the owner (`rwx`).
- The file is readable and executable by the group (`r-x`).
- The file is readable by others (`r--`).

---

### **3. Changing Permissions with `chmod`**

The `chmod` command is used to modify file permissions. You can change permissions using two methods: **numeric mode** or **symbolic mode**.

#### **Numeric Mode**:

Permissions are represented by numbers:

- `r = 4`
- `w = 2`
- `x = 1`

To set permissions, you add the values corresponding to the permissions you want:

- **7** (4 + 2 + 1) = `rwx` (read, write, execute)
- **6** (4 + 2) = `rw-` (read, write)
- **5** (4 + 1) = `r-x` (read, execute)
- **4** = `r--` (read only)

Example:

```bash
chmod 755 filename
```

This gives the owner `rwx`, the group `r-x`, and others `r-x`.

#### **Symbolic Mode**:

In symbolic mode, you use letters to represent permissions:

- **u** = user (owner)
- **g** = group
- **o** = others
- **a** = all users (owner, group, and others)

You can add (`+`), remove (`-`), or set exactly (`=`) the permissions.

Example:

```bash
chmod u+x filename      # Adds execute permission to the owner
chmod g-w filename      # Removes write permission from the group
chmod o+r filename      # Adds read permission to others
```

You can also combine these commands:

```bash
chmod u+x,g-w filename  # Adds execute to owner, removes write from group
```

---

### **4. Changing Ownership with `chown`**

The `chown` command is used to change the owner and/or group of a file or directory.

#### **Syntax**:

```bash
chown [owner][:group] filename
```

- **To change the owner**:

  ```bash
  sudo chown newuser filename
  ```

- **To change the owner and group**:

  ```bash
  sudo chown newuser:newgroup filename
  ```

- **To change the group only**:
  ```bash
  sudo chown :newgroup filename
  ```

#### Example:

To change the owner to `user1` and the group to `admins` for a file:

```bash
sudo chown user1:admins filename
```

To check the current ownership and permissions:

```bash
ls -l filename
```

---

### **5. Managing Special Permissions**

Linux also provides **special permissions** that can be applied to files and directories. These permissions are useful for managing specific scenarios and more advanced file access control.

#### **Setuid (`s`)**:

The **setuid** permission allows a program to run with the privileges of the owner, rather than the user running the program. It's mostly used for programs that need elevated permissions to perform specific tasks (like changing a user’s password).

To add the **setuid** permission:

```bash
chmod u+s filename
```

#### **Setgid (`s`)**:

The **setgid** permission works similarly to **setuid**, but it applies to the group. When set on a directory, files created within the directory inherit the group of the directory, not the user’s current group.

To add the **setgid** permission:

```bash
chmod g+s directoryname
```

#### **Sticky Bit (`t`)**:

The **sticky bit** ensures that only the owner of a file or directory can delete or rename it. Even if others have write permissions, they won’t be able to delete files they don’t own.

To add the **sticky bit** permission:

```bash
chmod +t directoryname
```

---

### **6. Managing Permissions for Directories**

Directory permissions are slightly different than file permissions. They control access to the directory itself (whether users can list its contents or add files to it).

- **Read (`r`)**: Allows the user to list the contents of the directory.
- **Write (`w`)**: Allows the user to create, delete, or rename files within the directory.
- **Execute (`x`)**: Allows the user to **enter** the directory (use the `cd` command).

To give a user access to a directory:

- **Full access** to a directory: `rwx`
- **Read and execute** but no write: `r-x`
- **Read-only** access to list files: `r--`

Example:

```bash
chmod 755 directoryname
```

This grants:

- **Owner**: `rwx`
- **Group**: `r-x`
- **Others**: `r-x`

---

### **7. Access Control Lists (ACLs)**

In certain cases, you may need more granular control over permissions than the basic owner/group/others model allows. **Access Control Lists (ACLs)** provide a way to specify permissions for individual users and groups.

To enable ACLs on a file or directory, you can use `setfacl` and `getfacl`.

- **Viewing ACLs**:

  ```bash
  getfacl filename
  ```

- **Setting ACLs**:
  You can add or modify ACLs for users and groups:

  ```bash
  setfacl -m u:username:rw filename  # Gives read and write to a specific user
  setfacl -m g:groupname:r-- filename  # Gives read-only to a specific group
  ```

- **Removing ACLs**:
  ```bash
  setfacl -x u:username filename
  ```

---

### **File Permissions and Ownership in Linux**

In Linux, file permissions and ownership control who can access and modify files and directories. The ability to control file permissions is essential for system security and user access management. Understanding how to assign and manage these permissions is crucial for Linux system administrators and regular users alike.

---

### **1. File Permissions in Linux**

Linux file permissions are divided into three categories: **user (owner)**, **group**, and **others**. Each category can be granted different levels of access to the file. The three basic permissions are:

- **Read (`r`)**: The ability to view the contents of a file.
- **Write (`w`)**: The ability to modify or delete the contents of a file.
- **Execute (`x`)**: The ability to run the file as a program or script.

#### **Understanding File Permissions Representation**

When you list the details of files or directories using the `ls -l` command, the output includes the file's permissions:

```bash
ls -l filename
```

Example output:

```
-rwxr-xr--
```

This string can be broken down as follows:

- **First Character**: Indicates the file type. Common types are:
  - `-`: Regular file
  - `d`: Directory
  - `l`: Symbolic link
- **Next Three Characters**: The owner's permissions (`rwx` means read, write, and execute).
- **Next Three Characters**: The group's permissions (`r-x` means read and execute).
- **Last Three Characters**: Others' permissions (`r--` means read only).

In the above example (`-rwxr-xr--`):

- The **owner** has `read`, `write`, and `execute` permissions.
- The **group** has `read` and `execute` permissions but cannot write to the file.
- **Others** can only `read` the file.

---

### **2. Changing File Permissions with `chmod`**

The `chmod` command (short for "change mode") is used to modify file permissions. There are two ways to use `chmod`: **numeric mode** and **symbolic mode**.

#### **Numeric Mode**

In numeric mode, you represent permissions with numbers. Each permission type is assigned a value:

- **Read (r) = 4**
- **Write (w) = 2**
- **Execute (x) = 1**

To modify permissions, you sum the values of the permissions you want to apply. The permissions are specified in three sets: owner, group, and others.

- **7** (4 + 2 + 1) = `rwx` (read, write, execute)
- **6** (4 + 2) = `rw-` (read, write)
- **5** (4 + 1) = `r-x` (read, execute)
- **4** = `r--` (read-only)
- **3** (2 + 1) = `wx` (write, execute)
- **2** = `w--` (write-only)
- **1** = `x--` (execute-only)

For example:

```bash
chmod 755 filename
```

This command grants:

- **Owner**: `rwx` (read, write, execute)
- **Group**: `r-x` (read, execute)
- **Others**: `r-x` (read, execute)

#### **Symbolic Mode**

In symbolic mode, you use letters to represent permissions. You can modify permissions using the following operators:

- **+**: Add permission
- **-**: Remove permission
- **=**: Set exact permission (overwrite existing permissions)

Example:

```bash
chmod u+x filename  # Add execute permission to the owner (u = user)
chmod g-w filename  # Remove write permission from the group (g = group)
chmod o+r filename  # Add read permission to others (o = others)
```

You can also combine changes:

```bash
chmod u+x,g-w filename  # Add execute permission to owner and remove write from group
```

---

### **3. File Ownership in Linux**

Each file or directory in Linux has an **owner** and a **group** associated with it. When a file is created, the user who creates it becomes the owner, and the file is assigned to the user's default group.

#### **Viewing Ownership**

To view the owner and group of a file, you can use the `ls -l` command:

```bash
ls -l filename
```

Example:

```
-rwxr-xr-- 1 user1 group1 4096 Jan 1 10:00 filename
```

This indicates:

- The **owner** of the file is `user1`.
- The **group** associated with the file is `group1`.

#### **Changing Ownership with `chown`**

The `chown` command is used to change the ownership of a file or directory. You can change the **owner**, the **group**, or both.

##### **Syntax**:

```bash
chown [newowner][:newgroup] filename
```

- To change only the owner:
  ```bash
  sudo chown newowner filename
  ```
- To change both the owner and the group:
  ```bash
  sudo chown newowner:newgroup filename
  ```
- To change the group only:
  ```bash
  sudo chown :newgroup filename
  ```

Example:
To change the owner of a file to `user2` and the group to `group2`:

```bash
sudo chown user2:group2 filename
```

---

### **4. Managing Permissions for Directories**

Permissions for directories differ slightly from those for files. While the basic permissions (`read`, `write`, and `execute`) still apply, the meaning of these permissions changes when applied to directories:

- **Read (`r`)**: Allows the user to list the contents of the directory (`ls`).
- **Write (`w`)**: Allows the user to add, remove, or rename files in the directory.
- **Execute (`x`)**: Allows the user to enter the directory (`cd`) and access files within it.

To give a user full access to a directory, you would grant `rwx` permissions to the owner, group, and others:

```bash
chmod 777 directoryname
```

This gives:

- **Owner**: `rwx`
- **Group**: `rwx`
- **Others**: `rwx`

---

### **5. Special Permissions**

In addition to the basic `rwx` permissions, Linux supports **special permissions** for more advanced control:

#### **Setuid (`s`)**

- When set on an executable file, the **setuid** permission causes the program to run with the privileges of the file's owner (usually root).
- Example:
  ```bash
  chmod u+s program
  ```

#### **Setgid (`s`)**

- When set on a directory, the **setgid** permission makes files created within the directory inherit the group of the directory, not the user's current group.
- Example:
  ```bash
  chmod g+s directory
  ```

#### **Sticky Bit (`t`)**

- The **sticky bit** is used on directories to prevent users from deleting files they do not own, even if they have write access to the directory.
- Example:
  ```bash
  chmod +t directory
  ```

---

### **6. Summary**

In Linux, **file permissions** control who can read, write, or execute a file, while **ownership** determines who owns a file and which group it belongs to. Permissions are critical for system security and can be modified using commands like `chmod`, `chown`, and `chgrp`. By understanding how to assign, change, and view file permissions and ownership, you can manage access to files and directories efficiently, ensuring secure access control in your Linux system.

### **Key Commands**:

- `ls -l`: View file permissions and ownership.
- `chmod`: Change file permissions.
- `chown`: Change file ownership.
- `chgrp`: Change the group ownership of a file.

### **User Management in Linux**

User management is a fundamental aspect of system administration in Linux. It involves creating, modifying, and deleting user accounts, as well as assigning and managing permissions to control access to resources. Linux provides various tools and commands to efficiently manage users and their access to the system.

In this guide, we will explore how to manage users, groups, and their permissions in Linux, ensuring that the system is secure and organized.

---

### **1. Types of Users in Linux**

In Linux, there are several types of users that can be managed:

- **Root User**: The root user is the superuser with unrestricted access to all files and commands on the system. This user has administrative privileges.
- **Regular Users**: These users have limited access to system resources. They can perform tasks like running programs and accessing files within their home directory.
- **System Users**: These users are created by the system for specific purposes, such as running services or processes (e.g., `nobody`, `daemon`).

---

### **2. Managing User Accounts**

#### **Creating a User**

The `useradd` command is used to create new users. It allows you to define the user’s home directory, shell, and group memberships.

##### **Syntax**:

```bash
sudo useradd [options] username
```

Example:

```bash
sudo useradd -m -s /bin/bash john
```

- `-m`: Creates the user's home directory if it doesn't exist.
- `-s`: Specifies the login shell for the user. In this example, it is `/bin/bash`.

After creating a user, you can set a password for them using the `passwd` command:

```bash
sudo passwd john
```

#### **Viewing User Information**

To view detailed information about a user, you can use the `id` command:

```bash
id username
```

This will display the user’s UID (User ID), GID (Group ID), and group memberships.

#### **Modifying User Accounts**

You can modify existing users with the `usermod` command.

##### **Common Options**:

- `-l`: Change the username.
- `-d`: Change the home directory.
- `-s`: Change the login shell.

Example:

```bash
sudo usermod -l johnny john
```

This changes the username from `john` to `johnny`.

#### **Deleting a User**

To remove a user account, use the `userdel` command.

##### **Syntax**:

```bash
sudo userdel [options] username
```

Example:

```bash
sudo userdel johnny
```

- To also remove the user's home directory and mail spool:
  ```bash
  sudo userdel -r johnny
  ```

---

### **3. Managing Groups**

In Linux, groups are used to organize users and manage permissions. Each user belongs to at least one group, and permissions can be assigned to a group rather than individual users.

#### **Creating a Group**

The `groupadd` command is used to create a new group.

##### **Syntax**:

```bash
sudo groupadd groupname
```

Example:

```bash
sudo groupadd developers
```

#### **Adding a User to a Group**

The `usermod` command can be used to add a user to a group.

##### **Syntax**:

```bash
sudo usermod -aG groupname username
```

Example:

```bash
sudo usermod -aG developers john
```

This adds the user `john` to the `developers` group.

#### **Deleting a Group**

To remove a group, use the `groupdel` command.

##### **Syntax**:

```bash
sudo groupdel groupname
```

Example:

```bash
sudo groupdel developers
```

---

### **4. Managing User Permissions**

User permissions in Linux determine what actions users can perform on files and directories. By controlling these permissions, you ensure that users have access only to the files and commands they need to perform their tasks.

#### **Understanding Permission Types**

- **Read (`r`)**: Allows the user to view the contents of the file.
- **Write (`w`)**: Allows the user to modify the file's contents.
- **Execute (`x`)**: Allows the user to run the file as a program or script.

Permissions can be set for:

- **Owner** (the user who owns the file).
- **Group** (users who belong to the file’s group).
- **Others** (all users on the system who are not the owner or in the group).

#### **Changing User Permissions**

To modify file permissions for a user, use the `chmod` command. For example:

```bash
chmod u+rwx file.txt
```

This command grants read, write, and execute permissions to the **owner** (user) of the file `file.txt`.

##### **Permissions for Groups and Others**

To grant permissions to the group or others, replace the `u` (user) with `g` (group) or `o` (others). For example:

```bash
chmod g+rx file.txt  # Add read and execute permissions to the group
chmod o-w file.txt    # Remove write permission from others
```

#### **Setting Ownership**

The `chown` command changes the owner and group of a file or directory. For example:

```bash
sudo chown john:developers file.txt
```

This changes the owner of `file.txt` to `john` and the group to `developers`.

---

### **5. Managing User Sessions**

Users can have different active sessions on the system, such as terminal sessions or remote logins. To manage user sessions:

#### **Viewing Active Users**

Use the `who` or `w` command to see who is currently logged into the system:

```bash
who
```

or

```bash
w
```

#### **Killing User Sessions**

If necessary, you can terminate a user's session using the `pkill` or `kill` command:

```bash
pkill -u username  # Kill all processes for a specific user
```

or

```bash
sudo kill -9 PID  # Kill a specific process by its Process ID (PID)
```

#### **Locking and Unlocking User Accounts**

You can lock a user account to prevent login with the `passwd` command:

```bash
sudo passwd -l username
```

To unlock the account:

```bash
sudo passwd -u username
```

---

### **6. Managing Sudo Access**

In Linux, `sudo` allows a user to perform administrative tasks. Only users who are members of the `sudo` or `wheel` group can run commands with `sudo` privileges.

#### **Adding a User to the `sudo` Group**

To grant a user sudo privileges, you can add them to the `sudo` or `wheel` group using `usermod`:

```bash
sudo usermod -aG sudo username
```

or

```bash
sudo usermod -aG wheel username
```

#### **Configuring `sudo` Access**

The `sudoers` file defines which users and groups have `sudo` access and what commands they can run. You can edit this file using the `visudo` command to ensure proper syntax:

```bash
sudo visudo
```

---

### **7. Security Considerations**

Managing users and their permissions is critical for securing a Linux system. A few best practices to follow include:

- **Regularly audit user accounts** to ensure that only active users have access.
- **Use the principle of least privilege**: grant users only the permissions they need.
- **Set strong passwords** and encourage users to change them regularly.
- **Limit `sudo` access** to trusted users who need administrative privileges.
- **Lock inactive accounts** and remove obsolete users.

---

### **8. Summary**

User management in Linux is a vital task for maintaining a secure and organized system. With the `useradd`, `usermod`, `userdel`, and related commands, system administrators can create, modify, and delete user accounts, manage group memberships, and assign appropriate file permissions.

By following best practices for user management and permissions, you can ensure that users have the appropriate level of access to system resources, keeping your Linux system both secure and efficient.

### **Key Commands**:

- `useradd`: Create a new user.
- `usermod`: Modify an existing user.
- `userdel`: Delete a user.
- `groupadd`: Create a new group.
- `usermod -aG`: Add a user to a group.
- `chown`: Change file ownership.
- `chmod`: Change file permissions.
- `passwd`: Set or modify a user’s password.
- `sudo`: Grant administrative privileges.

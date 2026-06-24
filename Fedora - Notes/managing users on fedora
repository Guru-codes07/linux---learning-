# Managing Users on Fedora

Linux is a multi-user operating system. User management allows administrators to create, modify, and manage user accounts.

---

# Current User Information

## whoami

Displays the currently logged-in user.

### Example

```bash
whoami
```

Output:

```text
guruprasad
```

---

## id

Displays detailed user information.

### Example

```bash
id
```

Output:

```text
uid=1000(guruprasad) gid=1000(guruprasad)
```

---

# View User Information

## who

Displays currently logged-in users.

### Example

```bash
who
```

---

## users

Displays logged-in usernames.

### Example

```bash
users
```

---

# Create a New User

### Syntax

```bash
sudo useradd <username>
```

### Example

```bash
sudo useradd testuser
```

---

# Set User Password

### Syntax

```bash
sudo passwd <username>
```

### Example

```bash
sudo passwd testuser
```

---

# Delete a User

### Syntax

```bash
sudo userdel <username>
```

### Example

```bash
sudo userdel testuser
```

---

# Delete User and Home Directory

### Syntax

```bash
sudo userdel -r <username>
```

### Example

```bash
sudo userdel -r testuser
```

---

# Groups

Groups help manage permissions for multiple users.

---

## View User Groups

```bash
groups
```

### Example

```text
guruprasad wheel docker
```

---

## Add User to Group

### Syntax

```bash
sudo usermod -aG <group> <username>
```

### Example

```bash
sudo usermod -aG wheel testuser
```

---

## Remove User from Group

```bash
sudo gpasswd -d testuser wheel
```

---

# Important System Files

### User Accounts

```bash
cat /etc/passwd
```

### Groups

```bash
cat /etc/group
```

---

# Summary

| Command     | Purpose                        |
| ----------- | ------------------------------ |
| whoami      | Current user                   |
| id          | User information               |
| who         | Logged-in users                |
| users       | Display usernames              |
| useradd     | Create user                    |
| passwd      | Set password                   |
| userdel     | Delete user                    |
| userdel -r  | Delete user and home directory |
| groups      | View groups                    |
| usermod -aG | Add user to group              |

Understanding users and groups is essential for Linux administration and permission management.


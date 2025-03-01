# 🛠️ Configure Git for Different User Profiles Based on Project Folders

This guide explains how to configure Git to automatically use different user details for projects inside specific directories.

---

## 📌 Overview

With this setup:

- **All projects inside the `folder1/` directory** will use **Keshav Gupta**'s Git credentials.
- **All projects inside the `folder2/` directory** will use **Lazy G**'s Git credentials.

This method ensures that you no longer need to manually switch users when working on different projects.

---

## 📖 Steps to Configure

### 🚀 Step 1: Open the Global Git Configuration File

Run the following command in the terminal:

```sh
nano ~/.gitconfig
```

📌 _For Windows users using Git Bash, use:_

```sh
notepad ~/.gitconfig
```

---

### 🚀 Step 2: Add Conditional Git Configurations

At the bottom of the `~/.gitconfig` file, add the following lines:

```ini
[includeIf "gitdir:~/folder1/"]
    path = ~/folder1/.gitconfig

[includeIf "gitdir:~/folder2/"]
    path = ~/folder2/.gitconfig
```

#### 📌 What This Does

- **`gitdir:~/folder1/`** → Applies settings to all Git repositories inside `~/folder1/`.
- **`gitdir:~/folder2/`** → Applies settings to all Git repositories inside `~/folder2/`.

✅ **Save the file**:

- If using **nano**, press `CTRL + X`, then press `Y`, and hit `ENTER`.

---

### 🚀 Step 3: Create a `.gitconfig` File for `folder1` Projects

Run:

```sh
nano ~/folder1/.gitconfig
```

Now, add this content:

```ini
[user]
    name = "Keshav Gupta"
    email = "guptakeshav1503@gmail.com"
```

✅ **Save the file** (`CTRL + X`, then `Y`, then `ENTER`).

---

### 🚀 Step 4: Create a `.gitconfig` File for `folder2` Projects

Run:

```sh
nano ~/folder2/.gitconfig
```

Add the following content:

```ini
[user]
    name = "Lazy G"
    email = "lazyg@gmail.com"
```

✅ **Save the file** (`CTRL + X`, then `Y`, then `ENTER`).

---

## 🔍 Step 5: Verify the Configuration

### ✅ Check Git User for a `folder1` Project

Run:

```sh
cd ~/folder1/project1  # Navigate to a project inside folder1
git config --get user.name
git config --get user.email
```

📌 **Expected Output:**

```
Keshav Gupta
guptakeshav1503@gmail.com
```

---

### ✅ Check Git User for a `folder2` Project

Run:

```sh
cd ~/folder2/project3  # Navigate to a project inside folder2
git config --get user.name
git config --get user.email
```

📌 **Expected Output:**

```
Lazy G
lazyg@gmail.com
```

---

## 🎯 Conclusion

With this setup, Git will automatically use the correct **user.name** and **user.email** based on the project directory. 🎉🚀

🔹 **No more manually switching Git credentials for different projects!**  
🔹 **Git now handles it automatically, based on where your project is located.**

---

## 📌 Additional Commands

### 🔄 Check All Git Configurations

```sh
git config --list --show-origin
```

This displays all configurations along with their source files.

### 🔄 Remove a Git Configuration (if needed)

To remove a global Git configuration:

```sh
git config --global --unset user.name
git config --global --unset user.email
```

To remove a local Git configuration (specific to a repository):

```sh
git config --local --unset user.name
git config --local --unset user.email
```

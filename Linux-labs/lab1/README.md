
# Lab 1: User and Group Configuration for Passwordless `sudo apt install nginx`

## Objective
In this lab, i will:
1. Create a user and a group.
2. Allow the user to run `sudo apt install nginx` without a password.
3. Ensure that all other `sudo` commands require a password.

---

## Steps

### 1. Create a Group
Create a new group called `ivolve`:
```bash
sudo groupadd ivolve
```
### 2. Create a User and Add to the Group
Create a new user called ranatalaat and add them to the ivolve group:
```bash
sudo useradd ranatalaat
sudo usermod -aG ivolve ranatalaat
```
### 3. Modify the sudoers File
Edit the sudoers file to allow members of the gnginx group to run sudo apt install nginx without a password:
```bash
sudo vim sudoers
```
Add the following line at the end of the file:
```bash
%ivolve ALL=(ALL) NOPASSWD: /usr/bin/apt install nginx
%ivolve ALL=(ALL) ALL

```
### 4. Test the Configuration
Switch to the ranatalaat account:

```bash
su ranatalaat
```
Run the following command to test if sudo apt install nginx works without a password:
```bash
sudo apt update
sudo apt install nginx
```
### output 
![install nginx](https://github.com/user-attachments/assets/ac63ec94-6800-4840-a5b7-7cb9c78cc69c)


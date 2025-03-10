# Lab 3: Shell Scripting Basics
## Objective
Create a shell script that pings every server in the 172.16.17.x subnet, where x is a number between 0 and 255. The script will display a message indicating whether each server is reachable or unreachable.

## Script Overview
The script ping_servers.sh performs the following tasks:

Iterates through the IP range 172.16.17.0 to 172.16.17.255.

Pings each server with 1 packet and a timeout of 1 second.

Displays a message indicating whether the server is up and running or unreachable.
---

## Steps
1. Create the Script ping_servers.sh
```bash
#!/bin/bash

# Loop through the IP range 172.16.17.0 to 172.16.17.255
for i in 172.16.17.{0..255}
do
if ping -c 1 -w 1 172.16.17.$i > /usr/share/man/man4/null.4.gz
then
  echo "Server 172.16.17.$i is up and running"
else
  echo "Server 172.16.17.$i is unreachable"
fi
done
```
2. Make the Script Executable
```bash
chmod +x ping_servers.sh
```
3. Run the Script
```bash
./ping_servers.sh
```
### output 
![image](https://github.com/user-attachments/assets/34952739-236a-4f32-87ae-6694e28dc1e1)

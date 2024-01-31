---
created: 2024-01-31T07:04
updated: 2024-01-31T22:00
---
Docker is a containerisation and virtualization tool that became popular in the 2010s as a lightweight alternative to running [[virtual machines]].



- 
## Network Issues
	- Experienced a problem where docker containers are not allowed to access stuff on the `192.168.x.x` subnet.
	- If this happens, you can empty iptables and restart docker:
	- ```shell
	  sudo service docker stop
	  
	  sudo iptables -P INPUT ACCEPT
	  sudo iptables -P FORWARD ACCEPT
	  sudo iptables -P OUTPUT ACCEPT
	  sudo iptables -t nat -F
	  sudo iptables -t mangle -F
	  sudo iptables -F
	  sudo iptables -X
	  
	  sudo service docker start
	  ```
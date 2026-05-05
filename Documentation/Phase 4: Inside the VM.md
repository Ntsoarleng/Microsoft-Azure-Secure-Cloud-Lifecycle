## The LAMP (Linux, Apache, MySQL, PHP) Stack

As already establisshed in Phade 3, whenever a session expire or has not been used for several hourse, Microsoft assigns a new IP Address to one's Azure Cloud Shell. Therefore, before installing the LAMP stack, I needed to get the newly assigned IP address, update the NSG rules, then ssh into the virtual machine.

Getting the IP Address and Updating the NSG rules:

<img width="1600" height="458" alt="ifconfig and NSG update 2" src="https://github.com/user-attachments/assets/0db0cc45-c8cb-47cb-86c5-7993881862f2" />

<br>

SSH-ing into the virtual machine:
<img width="1285" height="599" alt="ssh into vm2" src="https://github.com/user-attachments/assets/f8799e99-5ec0-4503-bfdb-c3bb4a0e82a0" />

<br>
Now that the setup for this next phase was done: successfully updated the NSG rules and SSHed into the virtual machine, the LAMP stack could then be installed.



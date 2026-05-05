## The LAMP (Linux, Apache, MySQL, PHP) Stack

As already establisshed in Phade 3, whenever a session expire or has not been used for several hourse, Microsoft assigns a new IP Address to one's Azure Cloud Shell. Therefore, before installing the LAMP stack, I needed to get the newly assigned IP address, update the NSG rules, then ssh into the virtual machine.

Getting the IP Address and Updating the NSG rules:

<img width="1600" height="458" alt="ifconfig and NSG update 2" src="https://github.com/user-attachments/assets/0db0cc45-c8cb-47cb-86c5-7993881862f2" />

<br>

SSH-ing into the virtual machine:
<img width="1285" height="599" alt="ssh into vm2" src="https://github.com/user-attachments/assets/f8799e99-5ec0-4503-bfdb-c3bb4a0e82a0" />

<br>
Now that the setup for this phase was done: successfully updated the NSG rules and SSHed into the virtual machine, the LAMP stack could be installed.

<br>
<br>

### LAMP Stack Overview:

Here, I installed the four pillars of the LAMP stack in one go. Firstly, I had to refresh the server's package list - this is like checking the latest menu before ordering food. Also, it is a standard best practice habit. Even if one is not installing anything new, running a refresh every now and then is like a health check for the server's awareness.

**Command used to refresh server list:**
```bash
sudo apt update
```

Result:

<img width="1285" height="309" alt="apt update" src="https://github.com/user-attachments/assets/7483c961-a660-41fa-9d72-4ac36e2eb5a2" />

<br>
Once the server sussessfully refreshed, I installed the LAMP Stack.

<br>

**Command used:**
```bash
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql -y
```
The command intalls:
1. Linux (Ubuntu 22.04): the secure, stable operating system acting as the base.
2. Apache: The web server software that handles requests from the internet and delivers my portfolio content to the user's browser.
3. MySQL: The database management system. It acts like the brain where all my site's data will be organized and stored.
4. PHP: The programming language that connects the previous three. It fetches data from the MySQL database and hands it to Apache to display on the screen.

I utilized the LAMP stack to transition from a managed service (WordPress.com) to a self-hosted environment, giving me full control over the security configurations and backend management.

Result:

<img width="1600" height="610" alt="LAMP install" src="https://github.com/user-attachments/assets/3176fa60-f8da-4e49-bbd1-92aab6aa2f79" />
<br>

The LAMP Stack successfully installed. To confirm this, I went to a new tab on web browser and pasted the public IP Address of my virtual machine.

Returned page:

<img width="1600" height="813" alt="apache default page" src="https://github.com/user-attachments/assets/4240a261-f8da-4ab7-92c9-27ccf110751a" />
<br>
This meant that my Linux server was officially talking to the world!

NOTE: upon accessing the VM's Public IP, the browser correctly flags the connection as "Not Secure".
- Root Cause: The server is currently communicating via HTTP (Port 80). Traffic sent over HTTP is unencrypted (plain text), which poses a risk of Man-in-the-middle (MITM) attacks where an adversary could intercept credentials. In this case, no credentials will be required. However, as a best practice, HTTPS must always be used.
- GRC Perspective: From a compliance standpoint, this is an identified vulnerability. However, since this is still the Development phase and I am using a raw IP Address rather than a registered domain, a trusted SSL/TLS certificate cannot be issued yet. This will all be mitigated as the project progresses.






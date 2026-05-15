## The LAMP (Linux, Apache, MySQL, PHP) Stack

As already established in Phade 3, whenever a session expires or has not been used for several hourse, Microsoft assigns a new IP Address to one's Azure Cloud Shell. Therefore, before installing the LAMP stack, I needed to get the newly assigned IP address, update the NSG rules, then ssh into the virtual machine.

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

<br>

### Setting up the Database

Here the MySQL database wordpress_db is provisioned to serve as the centralized repository for all the site metadata. This architectural choice supports Data Persistence and allows for granular Access Control Management by isolating application data from system-level database tables.

**Command used to crate the database:**
```bash
CREATE DATABASE wordpress_db;
```

Thereafter, I made syntax errors when creating the specific admin user. I fixed this by deleting all the mistakes I could've made and started afresh.

**Command used to create the specific admin user:**
```bash
CREATE USER 'portfolio_admin'@'localhost' IDENTIFIED BY 'CyberSecure_99!';
```

After the previous step, I linked the user to the database with the right permissions.

**Command used:**
```bash
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'portfolio_admin'@'localhost';
```

To save the changes,

**Command used:**
```bash
FLUSH PRIVILEGES;
```

To confirm if the database was created correcly,

**Command used:**
```bash
SHOW DATABASE;
```

Result:
<img width="1275" height="508" alt="sql database" src="https://github.com/user-attachments/assets/26f685ff-e029-4e7a-9d02-05e3e56c1655" />

<br>
The database and its permissions were configured successfully.

<br>

### Migration Prep

Here, I configured the wp-config.php file with restricted credentials. I downloaded the application and linked it to the infrastructure. It is baically like building the pipes before turning on the water.

To download and extract Wordpress,

**Commands used:**
```bash
cd ~
```
The above command retuns one to /home directory on the terminal.

```bash
wget https://wordpress.org/latest.tar.gz
```
The above command downloads the zipped Wordpress application.

```bash
tar -xzvf lastest.tar.gz
```

The above command extracts the application. At doing this, a lot of files and folders get returned to you on the terminal. This shows successful download and extraction.

<img width="1276" height="687" alt="wordpress workfiles" src="https://github.com/user-attachments/assets/94a2f60c-37ef-4870-8767-121e80443393" />


<br>

To move the files to the  Web Root,

**Command used:**

```bash
sudo cp -a wordpress/. /var/www/html/
```

After the above command, I had to connect this to the database by configuring the handshake.

**Commands used:**

```bash
cd /var/www/html/
```
The above command takes one and puts them in the /var/www/html/ directory.

```bash
sudo cp wp-config-sample.php wp-config.php
```

The above command copies the wp-config-sample.php file to wp-config.php

To open the wp-config.php file, the nano editor had to be opened in order to edit it and add the correct credentials that link this application to the database.

```bash
sudo nano wp-config.php
```

Result:

<img width="1600" height="698" alt="raw nano file" src="https://github.com/user-attachments/assets/1316ba6d-7777-4b75-bb01-3a5f0895d953" />
<br>

The modifications I made on the aboce screenshot:
1. DB_NAME = wordpress_db.
2. DB_USER = portfolio_admin.
3. DB_PASSWORD = CyberSecure_99!.

I then exited the nano editor by pressing CTRL + O, Enter, CTRL + X.

Lastly, to do security hardening, I set permissions.

**Commands used:**
```bash
sudo chown -R www-data:www-data /var/www/html/
```
```bash
sudo systemctl restart apache2
```

After this, I could then go to the web browser, put the public IP Address of the virtual machine, and it had to show the home page of the Wordpress application. However, that was not so. Instead, the default page of apache2 still showed:

<img width="1600" height="813" alt="apache default page" src="https://github.com/user-attachments/assets/a3cdfbce-2773-4140-b37d-27cd716c64fa" />

<br>

This happened because Apache2 is configured to prioritize index.html over index.php. The default Ubuntu istallation includes a placeholder index.html which took precedence over the WoordPress core files. 

I therefore listed all the files in that directory using the command:

```bash
ls -l
```

<img width="1287" height="500" alt="removing index html" src="https://github.com/user-attachments/assets/32c73f19-c481-46aa-873b-4977f15a1de9" />

<br>

At seeing that the second file listed after index.html was index.php, I removed index.html using the command:

```bash
sudo rm /var/www/html/index.html
```

This forced the web server to resolve the index.php file and make it the default.

I restarted apache2 again, and the result was:

<img width="1600" height="726" alt="wordpress configured" src="https://github.com/user-attachments/assets/3f7ac9a6-b5fc-4361-9a95-010586158ca6" />

<br>

The infrastructure to perform the WordPress website migration was successfully configured!

















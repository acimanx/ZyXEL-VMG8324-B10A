# ZyXEL-VMG8324-B10A

On latest firmwares ssh and telnet access is filtered to local user.
You can try to scan open ports of your device, for example with [nmap](https://nmap.org/).
If your device have SSH or Telnet ports open you can go directly to step 2.

### 1. Open telnet port

You can restore initial firmware by making factory reset 

> hold down the reset button until the power light turns red<sup>[1](#footnote1)</sup>

If you unable to connect automatically, set ip of your computer to usable host IP Range 192.168.1.2 - 192.168.1.254 with subnet mask 255.255.255.0 and gateway 192.168.1.1

For example:
|  |  |
|--|--|
| Adress: | 192.168.1.2 |
| Netmask: | 255.255.255.0 |
| Gateway: | 192.168.1.1 |

### 2. Telnet access
Using telnet client connect to 192.168.1.1
After successful connection login with **admin** and password **1234**.

### 3. Supervisor password

Executing in terminal:
`cat /etc/passwd`
we can get information for all user accounts on the system

Salt for the password is first 2 characters of the encrypted password.<sup>[2](#footnote2)</sup>
For example default login admin with password 1234 will be:
`admin:mTzCzri5uT0V.:100:1:Administrator:/:/bin/sh`
We can check that salt if first 2 characters by doing:
`openssl passwd -crypt -salt mT 1234`
and getting result:
`mTzCzri5uT0V.`

With this knowledge it is possible to decrypt password for supervisor account, but there is more easier way to do so: 

Executing:
`cat /var/csamu`
We will get pair user : password where password is base64 encoded value.
Using any base64 decoder we can receive our password values.

### 4. Securing from ISP, disabling firmware updates:
Using supervisor account we can have full access to our web system. 
1. In *maintance* -> *TR-069*
Disable inform
Change connection request settings

2. In *maintance* -> *Remote MGMT*
Check out all wan if present
3. Change supervisor password
4. ???

[1](#footnote1): http://lists.genieacs.com/pipermail/users/2015-July/000329.html

[2](#footnote2): https://forum.kitz.co.uk/index.php/topic,13930.msg351769.html#msg351769



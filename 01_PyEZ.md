# PyEZ
[Welcome to Junos PyEZ’s documentation!](https://junos-pyez.readthedocs.io/en/2.6.5/index.html)  - Module documentation  
[Junos PyEZ Source Code](https://github.com/Juniper/py-junos-eznc) - Github repo for PyEZ source code  
[Junos PyEZ library](https://github.com/Juniper/py-junos-eznc)  
[Use Junos PyEZ to Access the Shell on Junos Devices](https://www.juniper.net/documentation/us/en/software/junos-pyez/junos-pyez-developer/topics/task/junos-pyez-program-shell-accessing.html)  

This table lists the packages and libraries required to install Junos PyEZ on a CentOS Linux host.  

| **Packages** | 			**Description** |  
|    :---:     |                 :---      |  
| **pip**      | A utility used to install packages and modules from the Python package index.|
| **gcc**      | The GNU compiler collection of utilities and libraries.|
| **python-devel** |Header files, a static library and development tools for building Python modules, extending the Python interpreter, or embedding Python inapplications.|
| **libxml2-devel** | Development files for the GNOME XML library.|
| **libxslt-dev** | XML stylesheet transformation library development files.|
| **libssl-dev** | Part of the OpenSSL project's implementation of the SSL and Transport Layer Security (TLS) cryptographic protocols for secure communication over the Internet.|
| **libffi-devel** | Contains a foreign function interface that enables code written in one language to call codewritten in another language.|
| **openssl-dev** | The SSL development toolkit.|
| **redhat-rpmconfig** | Custom RedHat macros used to build RedHat Package Manager (RPM) packages |  

**Copy your public key to the junos device**  
Once the lab is active:

```
┌─[mhubbard@HP8600-150] - [~/GoogleDrive/04_Tools/AutoPWN-Suite]
└─[$] scp ~/.ssh/juniper_ed25519_key vector@66.129.234.214:/tmp
``` 

## Python Scripts

**Shell script to run cli commands**  
```
from jnpr.junos import Device
from jnpr.junos.utils.start_shell import StartShell

dev = Device(host='192.168.10.162', port='22', user='vector', password='H3lpd3sk')

ss = StartShell(dev)
ss.open()
uptime = ss.run('cli -c "show system uptime"')
sup_info = ss.run('cli -c "show system information"')
print(uptime[1])
print(sup_info[1])
ss.close()

```  

**Shell Script to list messages log file**  
``` 
from jnpr.junos import Device
from jnpr.junos.utils.start_shell import StartShell

dev = Device(host='192.168.10.162', port='22', user='vector', password='H3lpd3sk')

ss = StartShell(dev)
ss.open()
sofwareimage = ss.run('ls -ahl /var/log/messages')
print(sofwareimage[1])
ss.close()

```

**Script to SCP the messages log to the local computer**  
```
from jnpr.junos import Device
from jnpr.junos.utils.scp import SCP

dev = Device(host='192.168.10.162', port='22', user='vector', password='H3lpd3sk')
with SCP(dev, progress=True) as scp:
    scp.get('/var/log/messages', local_path='/users/mhubbard/Downloads/')

```

**Script to copy a file from the desktop to the switch /vat/tmp folder**  
```
from jnpr.junos.utils.scp import scp
from jnpr.junos import Device

dev = Device(host='66.129.234.214', port='33005',
             user='jcluser', password='Juniper!1')
with scp(dev, progress=True) as scp:
    scp.put('/users/mhubbard/Downloads/test.json', remote_path='/var/tmp')

```  

**Script to reboot the device**  
```
from jnpr.junos import Device
from jnpr.junos.utils.sw import SW

with Device(host='192.168.10.162', user='root', password='vPd4weOx62CfM12') as dev:
    sw = SW(dev)
    # immediate reboot
    print(sw.reboot())
    #  reboot in 5 minutes
    #  print(sw.reboot(in_min='5'))
    # reboot in at
    #  print(sw.reboot(at='23:00'))

```



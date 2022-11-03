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


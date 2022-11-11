# PyEZ
[Welcome to Junos PyEZ’s documentation!](https://junos-pyez.readthedocs.io/en/2.6.5/index.html)  - Module documentation  
[Junos PyEZ Developer Guide](https://www.juniper.net/documentation/us/en/software/junos-pyez/junos-pyez-developer/junos-pyez-developer.pdf)  
[Junos PyEZ Source Code](https://github.com/Juniper/py-junos-eznc) - Github repo for PyEZ source code  
[Junos PyEZ library](https://github.com/Juniper/py-junos-eznc)  
[Use Junos PyEZ to Access the Shell on Junos Devices](https://www.juniper.net/documentation/us/en/software/junos-pyez/junos-pyez-developer/topics/task/junos-pyez-program-shell-accessing.html)  
[Configuring JUNOS PyEZ Exception Handling](https://learningportal.juniper.net/juniper/resources/courses/__secure/jol_od/jncia-devops/IJAUT_JOL/IJAUT_OL_CH08/story_content/external_files/Configuring_Junos_PyEZ_Exception_Handling.pdf) - PDF containing a python example for error handling.  
[Transfer Files Using Junos PyEZ](https://www.juniper.net/documentation/us/en/software/junos-pyez/junos-pyez-developer/topics/task/junos-pyez-program-files-transferring-scp.html) - Include code to show progress.  
[PyEZ Examples](https://github.com/vnitinv/pyez-examples) - Blogs and sample code on github.  
[Getting Started with Juniper and Ansible](https://pynet.twb-tech.com/blog/getting-started-with-juniper-and-ansible.html) - Kirk Byers blog  s

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

### Copy python scripts to the Juniper vLab Ubuntu VM
I wasn't able to get the PyEZ scp script to pass a custom port so I couldn't run my python scripts from my MacBook. I decided to copy all of my scripts to the home/jcluser/JUNOS_PyEZ_AUTOMATION folder. It's better to edit the scripts to use the 100.123.1.0 IP address in VS Code before you copy them over. 

I used scp to copy them to the lab PyEZ VM.  

NOTE: The P is a capital P.

```
sscp -P 40010  ~/GoogleDrive/04_Tools/junos-pyez/*.py jcluser@66.129.234.214:/home/jcluser/JUNOS_PyEZ_AUTOMATION                                                                                                       
jcluser@66.129.234.214's password:
Get_version.py                                                                                                                                                                                       100% 3248    56.7KB/s   00:00
Interface_Flap_Detection.py                                                                                                                                                                          100% 5849   103.8KB/s   00:00
Juniper-route.py
```  

Now I can run the scripts against the virtual Juniper devices in the lab.

### Editing the scripts

To edit a script named Juniper-route.py  
```
jcluser@jet-vm:~/JUNOS_JET_AUTOMATION$ nano Juniper-route.py
```  

If you haven't used nano before, there are plenty of tutorials on the Internet. The basic commands you need are:  
ctrl+x - Exit. You will be  prompted to save any changes you made. Enter y, then confirm the file name.  
ctrl+w - Search  

### Make the script executable  
If you want to be able to run the scripts without prefacing them with python3 you will need to make them executable:  

`jcluser@pyez-vm:~/JUNOS_PyEZ_AUTOMATION$ chmod +x *.py`  

Then use ls -l to verify  
```
jcluser@pyez-vm:~/JUNOS_PyEZ_AUTOMATION$ ls -l
total 108
-rwxrwxrwx 1 jcluser jcluser 3217 Mar 28  2019 backup.conf
-rwxrwxrwx 1 jcluser jcluser  620 Mar 28  2019 Config_rollback.py
-rwxrwxrwx 1 jcluser jcluser  673 Mar 28  2019 File_list.py
-rwxrwxrwx 1 jcluser jcluser  818 Mar 28  2019 Get_device_config.py
-rwxrwxrwx 1 jcluser jcluser  771 Mar 28  2019 Get_interface_information.py
-rwxr-xr-x 1 jcluser jcluser 3248 Nov 10 17:28 Get_version.py
-rwxr-xr-x 1 jcluser jcluser 5849 Nov 10 17:28 Interface_Flap_Detection.py
-rwxr-xr-x 1 jcluser jcluser  346 Nov 10 17:28 jumiper-shell-cli.py
-rwxr-xr-x 1 jcluser jcluser  434 Nov 10 17:28 juniper-active-config.py
``` 

Notice the x in each file. That means it is executable.  

### Find out where Python 3 is installed  
You will need to have the shebang (#!/path to python) at the top of your script. To find out where python is installed use:  
```
jcluser@pyez-vm:~/JUNOS_PyEZ_AUTOMATION$ which python3
/usr/bin/python3
```  

So the shebang will be:  
`/usr/bin/python3`    

Now you can just type:  
`./Juniper-route.py`  

to run the script.  

### Conclusion
It seems like a lot of work but the VM will be the same everytime so you know the shebang and you can use these commands to set everything up:  
```  
cd JUNOS_PyEZ_AUTOMATION/
chmod +x *.py
ls -l
```  

Eazy Peasy.



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
from jnpr.junos.utils.scp import SCP
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








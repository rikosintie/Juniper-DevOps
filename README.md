# Juniper-DevOps
Juniper DevOps Certification information


[Course Outline](https://learningportal.juniper.net/juniper/resources/courses/__secure/jol_od/jncia-devops/IJAUT_JOL/IJAUT_OL_CH01/story_content/external_files/Course%20Outline.pdf)  
[Exam Objectives](https://www.juniper.net/us/en/training/certification/tracks/devops/jncia-devops.html?tab=jnciadevops) 


**Juniper Knowledgebase Articles**

* [XPath Terminology](https://www.w3schools.com/xml/xpath_nodes.asp)  
[JSNAPY](https://github.com/Juniper/jsnapy)  
* [Junos PyEZ Developer Guide](https://www.juniper.net/documentation/us/en/software/junos-pyez/junos-pyez-developer/index.html)  
* [Authenticate Junos PyEZ Users](https://www.juniper.net/documentation/us/en/software/junos-pyez/junos-pyez-developer/topics/topic-map/junos-pyez-authentication.html#id-authenticating-the-user-using-passwordprotected-ssh-key-files)  
* [Examples of using the Docker image](https://github.com/Juniper/py-junos-eznc/blob/master/DOCKER-EXAMPLES.md)  
* [Junos PyEZ](https://www.juniper.net/documentation/product/us/en/junos-pyez/) - Start here to evaluate, install, or use the Juniper Networks® Junos® PyEZ, a Python microframework that enables you to manage and automate devices running Junos OS.  
* [DAY ONE:JUNOS® PyEZCOOKBOOK](https://www.juniper.net/documentation/en_US/day-one-books/DO_PyEZ_Cookbook.pdf)  
* [Automation Forum](http://forums.juniper.net/t5/Automation/tkb-p/Automation_Scripting) -  The Automation Forum on the Juniper Tech Wiki is a great place to seek help and see more script examples.  

### XML  
The Junos XML protocol server is integrated into the Junos operating system and does not appear as a separate entry in process listings. The Junos XML protocol server directs the request to the appropriate software modules within the device, encodes the response in Junos XML protocol and Junos XML API tag elements, and returns the result to the client application.  

### Document Type Definition  
A file called a **document type definition**, or DTD, lists every tag element that can appear in the document or data set, defines the parent-child relationships between the tags, and specifies other tag characteristics. The same DTD can apply to many XML documents or data sets.

[XML Overview](https://www.juniper.net/documentation/us/en/software/junos/automation-scripting/topics/concept/junos-script-automation-xml-overview.html) - Start here if you are new to XML  
[XSLT Overview](https://www.juniper.net/documentation/us/en/software/junos/automation-scripting/topics/concept/junos-script-automation-xslt-overview.html) - Commit Scripts, operation scripts and SNMP scripts can be written in eXtensible Stylesheet Language Tranformations (XSLT).  
[Automation Scripting User Guide](https://www.juniper.net/documentation/us/en/software/junos/automation-scripting/index.html)  
[Junos XML API Explorer - Configuration Tags](https://apps.juniper.net/xmlapi/#)  



### Virtual Labs
* [Virtual labs for automation](https://jlabs.juniper.net/vlabs/portal/index.page) - Scroll down to the automation section.  
* [vLab Sandbox: PyEZ for Junos – Instructions](https://jlabs.juniper.net/vlabs/portal/pyez-for-junos/pyez-for-junos-instructions.page) - Instructions for running the PyEZ scripts in the lab.

Vlab instructions  
**On-box (vMX device)**  
Login to router R1.  

To view a list of available PyEZ apps, enter the following operational command:  
`request extension-service start ?`  

To execute a PyEZ app, enter the following operational command:
`request extension-service start <app-name>`

**Off-box (Ubuntu Linux server)**  
Login to server pyez-vm  
Go to /home/jcluser/JUNOS_PyEZ_AUTOMATION  
Type ls to view the available PyEZ apps  

To run an app, enter the following command:  
`python <app-name> <arguments>`  

To see which arguments are required, see the Command Samples and Syntax section of this page, or enter the following command:  
`python <app-name> -h`  

**Protip** - NETCONF must be enabled (it runs on port 830), before PyE can connect. Use this command to verify:
`show configuration system services netconf`


###Command Samples and Syntax

When running the PyEZ apps off-box, from the Ubuntu Linux server, additional parameters must be included.  

**Below are command syntax examples for each PyEZ app.**
python Pyez-tester.py -device 100.123.1.0 -user jcluser -password 'Juniper!1'  
python Get_device_config.py -device 100.123.1.0 -user jcluser -password 'Juniper!1' -output_format set
python Load_configuration.py -device 100.123.1.0 -user jcluser -password 'Juniper!1'  
python Get_interface_information.py -device 100.123.1.0 -user jcluser -password 'Juniper!1' -interface lo0  
python Config_rollback.py -device 100.123.1.0 -user jcluser -password 'Juniper!1'  
python File_list.py -device 100.123.1.0 -user jcluser -password 'Juniper!1' -path /var/db/scripts/jet/    

**Command Arguments:**  
* -device => Router R1’s management interface IP address  
* -user => Router R1’s user name  
* -password => Router R1’s user password  
* -path => Router R1’s shell path to list the files from  
* -output_format => Output format: set, json, txt, or unicode  



git clone git@git.cloudlabs.juniper.net:shantabain/PyEZ_config  
cd PyEZ_config  
ansible-playbook install-config-to-device.yml  
cd PLAYBOOK/  
ansible-playbook install-ansible2-6-4-to-device.yml  
ansible-playbook install-script-to-device.yml  

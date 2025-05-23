check version:
`snort -V`

test configuration and identify config file
`snort -c  /etc/snort/snort.conf -T`
`-c` specifies the config file
`-T` use for testing configuration file 
`-q` quiet mode

The configuration file is an all-in-one management file of the snort. 
* Rules 
* plugins 
* detection mechanisms
* default actions 
* and output settings 
are identified here. 
It is possible to have multiple configuration files for different purposes and cases but **can only use one at runtime.**


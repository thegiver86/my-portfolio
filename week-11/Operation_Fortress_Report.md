** Egress Drop Rule** 
iptables -A OUTPUT -d 198.51.100.0/24 -j DROP

**Suricata Rule**
alert tcp any any -> any 80 (msg:"Web Shell Execution Detected"; content:"cmd=whoami"; sid:1000001; rev:1;)

**Sysmon commandline rule**
<CommandLine condition="contains">curl http://198.51.100.5</CommandLine>


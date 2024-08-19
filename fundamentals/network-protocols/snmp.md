# SNMP

Get the MIBs

```bash
sudo apt install snmp-mibs-downloader
```

Enumerate with MIBs

```bash
#Big chunk
snmpwalk -v 2c -c public 10.10.10.92
#Process
snmpbulkwalk -v2c -c public 10.10.10.92 hrSWRunName
#Within the process
snmpbulkwalk -v2c -c public 10.10.10.92 hrSWRunTable | grep <PID>
#Interfaces
snmpbulkwalk -v2c -c public 10.10.10.92 ipAddressType
```

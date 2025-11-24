# STEP 1:  Integrate VirusTotal with the Wazuh manager

Su wazuh-server da terminale ho digitato:
```bash
sudo nano /var/ossec/etc/ossec.conf
```

 **inserito questo blocco**
 ```bash
 <integration>
   <name>virustotal</name>
   <api_key>**PERSONAL_API_KEYS _VIRUSTOTAL**</api_key>
   <rules_id>100200,100201</rules_id>
   <alert_format>json</alert_format>
  </integration>
```

ssh-keygen -f C:\Users\enris\.ssh\known_hosts -R 192.168.1.4


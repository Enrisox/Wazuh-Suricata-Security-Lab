# STEP 1:  Integrate VirusTotal with the Wazuh manager

On the WAZUH-SERVER terminal
```bash
sudo nano /var/ossec/etc/ossec.conf
```

 **I inserted this block**
 ```bash
 <integration>
   <name>virustotal</name>
   <api_key>PERSONAL_API_KEYS _VIRUSTOTAL</api_key>
   <rules_id>100200,100201</rules_id>
   <alert_format>json</alert_format>
  </integration>
```

 **<rule_id>100200,100201</rule_id>**: represents the rule that triggers the VirusTotal inspection. In this case, we have rule ID 100200 and 100201. I haven't created these rules yet so I wrote these rules to detect file changes in a specific folder of the endpoint. 


## LET'S CREATE THE WAZUH RULE ON WAZUH MANAGER

I wanted to trigger VT scanning only when any file was changed, deleted or added to avoid "bilions" of false positive alerts.

**A File Integrity Monitoring (FIM) it's a security technology that monitors files on a system to detect unauthorized changes.
Typically used in Intrusion Detection and Prevention Systems (IDS/IPS) and platforms like Wazuh or OSSEC.
It monitors attributes such as:

* File creation / deletion
* Content modification
* Permission or ownership changes
* File hashes or checksums
 ```bash
sudo nano /var/ossec/etc/ossec.conf
 ```
![Wazuh alert](img/img25.png)
<br>

**Search for the syscheck block.**
I then added this line for /root immediately after the other <directories> entries:
 ```bash
<directories check_all="yes" report_changes="yes" realtime="yes">/root</directories>
 ```
Ctrl+X

**Restart the Wazuh agent:**

 ```bash
sudo systemctl restart wazuh-agent
 ```

**Expected result<br>
Any changes in /root (file creation, modification, deletion) will trigger a Wazuh alert. <br>**

The corresponding alerts will have rule IDs 100200 and 100201 as indicated.

Step 1: Create the Malware "Cage" (Ubuntu VM)
Open the terminal on your Ubuntu VM (the agent) and run these commands:
 ```bash
# 1. Create the temporary folder
sudo mkdir -p /tmp/malware

# 2. Grant permissions to everyone (Read/Write/Execute)
sudo chmod 777 /tmp/malware
 ```

(Note: The /tmp folder is cleared every time you restart the PC. This is fine for testing, but if you want a permanent folder, create it in your home directory).
On the Manager (Wazuh OVA VM)
Here we tell Wazuh: "If someone touches the files, ask VirusTotal if they are infected."
Open the Wazuh VM console and edit the file:
 ```bash
sudo nano /var/ossec/etc/ossec.conf
 ```

Scroll down (or use CTRL+W to search for <global>). Paste this block just before the final </ossec_config> line.
 ```bash
<integration>
  <name>virustotal</name>
  <api_key>PASTE_YOUR_API_KEY_HERE</api_key>
  <group>syscheck</group>
  <alert_format>json</alert_format>
</integration>
 ```
Agent Port Configuration (Crucial)
Add/Verify the <remote> block to enable listening on TCP port 1514. Note: This must be placed outside the <global> block.

 ```bash
<remote>
  <connection>secure</connection>
  <port>1514</port>
  <protocol>tcp</protocol>
  <queue_size>131072</queue_size>
</remote>

 ```
Realtime FIM Activation:
In the <syscheck> section, add the specific folder:

 ```bash
<directories realtime="yes" check_all="yes">/tmp/malware</directories>
 ```
Save (CTRL+O, Enter) and Exit (CTRL+X).
Restart the Manager to apply changes:

 ```bash
sudo systemctl restart wazuh-manager
 ```




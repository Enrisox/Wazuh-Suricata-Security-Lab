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


Esatto, hai intuito bene la logica.

Il tutorial ti fa creare una cartella specifica (es. /tmp/malware) e dare permessi massimi (777) per due motivi tattici molto intelligenti per un ambiente di test:

Risparmiare le API di VirusTotal: Come ti dicevo, la licenza gratuita ti dà solo 4 controlli al minuto. Se tu dicessi a Wazuh di controllare "Tutto il computer", finiresti le API in un secondo (basta che il sistema aggiorni un log o scarichi un aggiornamento). Facendolo guardare solo in quella cartella, sei sicuro che VirusTotal verrà interpellato solo quando TU metti un file lì dentro.

Permessi Facili (777): Dare chmod 777 significa "chiunque può scrivere qui". In un tutorial è comodo perché puoi scaricare virus con il tuo utente, con root o con script automatici senza mai avere errori di "Permesso negato".

Ecco come replicare esattamente quel passaggio del tutorial sulla tua VM Ubuntu, integrandolo con la configurazione locale che è più semplice.

Passo 1: Crea la "Gabbia" per i Malware (VM Ubuntu)
Apri il terminale della tua VM Ubuntu (l'agente) e dai questi comandi:

# 1. Crea la cartella temporanea
sudo mkdir -p /tmp/malware

# 2. Dai i permessi a tutti (Lettura/Scrittura/Esecuzione)
sudo chmod 777 /tmp/malware
(Nota: La cartella /tmp si svuota ogni volta che riavvii il PC. Per i test va benissimo, ma se vuoi una cartella fissa, falla nella tua home).

Sul Manager (VM Wazuh OVA)
Qui diciamo a Wazuh: "Se qualcuno tocca i file, chiedi a VirusTotal se sono infetti".

Apri la console della VM Wazuh e edita il file:

sudo nano /var/ossec/etc/ossec.conf
Scorri verso il basso (o usa CTRL+W per cercare <global>). Incolla questo blocco subito prima della riga finale </ossec_config>.

⚠️ IMPORTANTE: Cancella INCOLLA_QUI_LA_TUA_API_KEY e metti la tua stringa lunga di VirusTotal.


<integration>
  <name>virustotal</name>
  <api_key>INCOLLA_QUI_LA_TUA_API_KEY</api_key>
  <group>syscheck</group>
  <alert_format>json</alert_format>
</integration>


Configurazione Porta Agenti (Cruciale) Aggiunto/Verificato il blocco <remote> per abilitare l'ascolto sulla porta 1514 TCP. Nota: Va posizionato fuori dal blocco <global>.

<remote>
  <connection>secure</connection>
  <port>1514</port>
  <protocol>tcp</protocol>
  <queue_size>131072</queue_size>
</remote>

Attivazione FIM Realtime: Nella sezione <syscheck>, aggiunta la cartella specifica:

XML

<directories realtime="yes" check_all="yes">/tmp/malware</directories>

Salva (CTRL+O, Invio) ed Esci (CTRL+X).


Riavvia il Manager per applicare:

sudo systemctl restart wazuh-manager 

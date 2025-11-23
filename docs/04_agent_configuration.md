# Wazuh Agent Configuration (Ubuntu)

## Install & enroll the agent
Commands:
```bash
sudo systemctl restart wazuh-agent
sudo /var/ossec/bin/agent-auth -m 192.168.x.x -A ubuntu-endpoint

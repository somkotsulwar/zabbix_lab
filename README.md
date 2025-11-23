# zabbix_automation_lab

# Zabbix Agent — Ansible Role

Deploy and configure **Zabbix Agent** on Linux hosts.

## Features

- Installs **zabbix-agent**
- Configures `Server` and `ServerActive`
- One liner execution.

## Installation steps.
#### Step1: Clone the repository
git clone https://github.com/somkotsulwar/zabbix_automation_lab.git
cd zabbix_automation_lab

#### Step 2: Update the inventory
Edit ems_inv.yml and add the target servers under zabbix_agents group or individually 
for ex. 
[zabbix_agents]

server1

server2

#### Step 3: Review the Zabbix Agent Template 
Located at roles/zabbix-agent/templates/zabbix_agentd.conf.j2

#### Step 5: Run the Ansible Playbook
ansible-playbook -i ems_inv.yml install_agent.yml 

#### Step 6: Add the Host in Zabbix Server

Before the agent can appear in monitoring, you must add the host in Zabbix:

1. Go to **Configuration → Hosts → Create host**
2. Set `Hostname` to match your Ansible inventory hostname
3. Add it to a Host Group (example: Linux servers)
4. Add an Agent interface with the server's IP and port 10050
5. Link a template such as **Template OS Linux by Zabbix agent**, **Linux by SNMP Template**
6. Save

#### Step 7: Verify Agent Connectivity

After saving, open **Monitoring → Hosts**.

You should see:

- Green **ZBX** availability
- Items and metrics latest data updating
######################################################################

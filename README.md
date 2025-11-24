### Repo zabbix_automation_lab used for auto deploy agent in zabbix on RHEL & Ubuntu.

#### Zabbix Agent — Ansible Role

Deploy and configure **Zabbix Agent** on Linux hosts.

#### Features

- Installs **zabbix-agent**
- Configures `Server` and `ServerActive`
- Deploys dynamic configuration using Jinja2 template
- Validates that the Zabbix agent service is active
- One-command execution (ansible-playbook -i inv.yml install_agent.yml)

Role Structure

```text
zabbix_automation_lab/
│
├── install_agent.yml
├── ems_inv.yml
│
├── group_vars/
│   └── all.yml
│
└── roles/
    └── zabbix-agent/
        ├── defaults/
        │   └── main.yml
        │
        ├── tasks/
        │   ├── main.yml
        │   ├── redhat.yml
        │   └── ubuntu.yml
        │
        ├── handlers/
        │   └── main.yml
        │
        ├── templates/
        │   └── zabbix_agentd.conf.j2
```


    
### Installation steps.
#### Step1: Clone the repository
git clone https://github.com/somkotsulwar/zabbix_automation_lab.git

cd zabbix_automation_lab

#### Step 2: Update the inventory
Edit ems_inv.yml and add the target servers under zabbix_agents group or individually 
for ex. 

[zabbix_agents]

server1/ip

server2/ip

#### Step 3: Review the Zabbix Agent Template 
Located at roles/zabbix-agent/templates/zabbix_agentd.conf.j2

#### Step 4: Run the Ansible Playbook 
ansible-playbook -i ems_inv.yml install_agent.yml 

Once completed successfully, you should see:

zabbix-agent service started and enabled


#### Step 5: Add the Host in Zabbix Server

Before the agent can appear in monitoring, you must add the host in Zabbix:

1. Go to **Configuration → Hosts → Create host**
2. Set `Hostname` to match your Ansible inventory hostname
3. Add it to a Host Group (example: Linux servers)
4. Add an Agent interface with the server's IP and port 10050
5. Link a template such as **Template OS Linux by Zabbix agent**, **Linux by SNMP Template**
6. Save

#### Step 6: Verify Agent Connectivity

After saving, open **Monitoring → Hosts**.

You should see:

- Green **ZBX** availability
- Items and metrics latest data updating

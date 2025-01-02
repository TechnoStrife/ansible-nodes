
### Inventory
Make inventory file `servers.yaml` with group `nodes`
```yaml
prometheus:
  hosts:
    <hostname>:
      ansible_host: <ip>
      ansible_user: root
      telegram_bot_token: <bot_token>
      telegram_chat_id: <chat_id>

nodes:
  hosts:
    srv1:
      ansible_host: <ip>
      ansible_user: root
      cysic_wallet: "0x..."
```

### Get collections
```
ansible-galaxy install -f -r roles/requirements.yml
```

### Setup
#### Prometheus
```
ansible-playbook -v prometheus.yaml -i ../servers.yaml --user root
```

#### prometheus node exporter
```
ansible-playbook -v prom-exporter.yaml -i ../servers.yaml --user root
```

#### cysic
```
ansible-playbook -v cysic.yaml -i ../servers.yaml --user root
```

#### rivalz
```
ansible-playbook -v rivalz.yaml -i ../servers.yaml --user root
```

Then manually:
	`rivalz change-wallet <wallet addr>`
	`rivalz change-hardware-config`
	`systemctl restart rivalz`
	`systemctl status rivalz`


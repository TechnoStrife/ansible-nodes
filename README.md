
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

fiamma:
  hosts:
    srv1:
```

### Get collections
```bash
ansible-galaxy install -f -r roles/requirements.yaml
```

### Setup
#### Prometheus
```bash
ansible-playbook -v prometheus.yaml -i ../servers.yaml --user root
```

#### prometheus node exporter
```bash
ansible-playbook -v prom-exporter.yaml -i ../servers.yaml --user root
```

#### Fiamma
```bash
ansible-playbook -v fiamma.yaml -i ../servers.yaml --user root
```

Then manually:
- `fiammad keys add $WALLET_NAME`
  Write down the mnemonic phrase.
  To recover the wallet later: `fiammad keys add --recover $WALLET_NAME`
- `systemctl restart fiamma`

#### cysic
```bash
ansible-playbook -v cysic.yaml -i ../servers.yaml --user root
```
When installing on VPS, first change the machine-id:
```bash
sudo rm /etc/machine-id
sudo systemd-machine-id-setup
```

#### rivalz
```bash
ansible-playbook -v rivalz.yaml -i ../servers.yaml --user root
```

Then manually:
	`rivalz change-wallet <wallet addr>`
	`rivalz change-hardware-config`
	`systemctl restart rivalz`
	`systemctl status rivalz`


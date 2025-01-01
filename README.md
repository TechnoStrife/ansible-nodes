
### Inventory
Make inventory file `servers.yaml` with group `nodes`
```yaml
nodes:
  hosts:
    server1:
      cysic_wallet: "0x..."
```


### Setup
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


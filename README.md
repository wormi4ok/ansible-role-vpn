# Ansible Role: VPN

Configure Wireguard VPN on Ubuntu servers.

This role installs a Wireguard VPN on the remote Ubuntu server and generates client configuration files locally. 

## Requirements

`qrencode` to show configs as QR codes

## Role Variables

All variables are defined in `defaults/main.yml`


| name | description | default value |
|------|-------------|---------------|
| vpn_keys_path | Local path to VPN config files | `configs/{{ vpn_server }}/wireguard` |
| vpn_server | VPN server real IP | `{{ ansible_default_ipv4.address }}`
| vpn_network | VPN subnet | `10.20.0.0/24` |
| vpn_port | UDP port (Random port is generated once per host) | `random(seed=inventory_hostname)` |
| vpn_dns_servers | DNS servers to use | `176.103.130.130`, `1.1.1.1` |
| vpn_clients | A list of client configuration names | `wg_{{ vpn_server }}` |
| force | Recreate all configs | `False` |

## Dependencies

No dependencies

## Example Playbook

```
- hosts: servers
  roles:
     - { role: wormi4ok.vpn, become: yes }
``` 

## Testing

```
docker run --rm -it \
    -v "$(pwd)":/tmp/$(basename "${PWD}"):ro \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -w /tmp/$(basename "${PWD}") \
    quay.io/ansible/molecule:3.0.8 \
    molecule test
```

## License

MIT

## Author Information

wormi4ok

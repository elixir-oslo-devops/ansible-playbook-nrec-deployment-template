# Main inventory

Example inventory in ini format:

```ini
[webservers]
web1 ansible_user=your_user ansible_ssh_private_key_file=/path/to/private_key
web2 ansible_user=your_user ansible_ssh_private_key_file=/path/to/private_key

[dbservers]
db1 ansible_user=your_user ansible_ssh_private_key_file=/path/to/private_key
```

Example inventory in YAML format:

```yaml
all:
  children:
    webservers:
      hosts:
        web1:
          ansible_user: your_user
          ansible_ssh_private_key_file: /path/to/private_key
        web2:
          ansible_user: your_user
          ansible_ssh_private_key_file: /path/to/private_key
    dbservers:
      hosts:
        db1:
          ansible_user: your_user
          ansible_ssh_private_key_file: /path/to/private_key
```
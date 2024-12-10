# ansible-playbook-nrec-deployment-template


# Building inventory

## Organising inventory

To organize your Ansible inventory, place your connection information within the inventory directory. 

For variables related to groups, use the group_vars directory and create files or subdirectories named after each group to store the group-specific variables. 

Similarly, for variables related to individual hosts, use the host_vars directory and create files or subdirectories named after each host to store the host-specific variables. This structure ensures that your inventory is well-organized and variables are easily accessible and manageable.


### Main inventory

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

## Variable precedence

> Ansible does apply variable precedence, and you might have a use for it. Here is the order of precedence from least to greatest (the last listed variables override all other variables):
>
> 1. command line values (for example, -u my_user, these are not variables)
> 2. role defaults (as defined in Role directory structure) 1
> 3. inventory file or script group vars 2
> 4. inventory group_vars/all 3
> 5. playbook group_vars/all 3
> 6. inventory group_vars/* 3
> 7. playbook group_vars/* 3
> 8. inventory file or script host vars 2
> 9. inventory host_vars/* 3
> 10. playbook host_vars/* 3
> 11. host facts / cached set_facts 4
> 12. play vars
> 13. play vars_prompt
> 14. play vars_files
> 15. role vars (as defined in Role directory structure)
> 16. block vars (only for tasks in block)
> 17. task vars (only for the task)
> 18. include_vars
> 19. set_facts / registered vars
> 20. role (and include_role) params
> 21. include params
> 22. extra vars (for example, -e "user=my_user")(always win precedence)

[See documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html#ansible-variable-precedence)
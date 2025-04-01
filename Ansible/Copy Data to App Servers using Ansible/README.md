## Task Overview

The Nautilus DevOps team needs to copy data from the jump host to all application servers in Stratos DC using Ansible. Execute the task with the following details:

a. Create an inventory file `/home/thor/ansible/inventory` on jump\_host and add all application servers as managed nodes.

b. Create a playbook `/home/thor/ansible/playbook.yml` on the jump host to copy the `/usr/src/sysops/index.html` file to all application servers, placing it at `/opt/sysops`.

**Note:** Validation will run the playbook using the command:

```bash
ansible-playbook -i inventory playbook.yml
```

Ensure the playbook functions properly without any extra arguments.

---

## Implementation Details

### 1. Creating the Inventory File

The inventory file (`inventory`) contains details of the application servers:

### 2. Creating the Ansible Vault for Passwords

Since SSH passwords are sensitive information, i used **Ansible Vault** to store them securely.

#### Encrypting Passwords:

Create a file `group_vars/application_servers/vault.yml` with the following content before encryption:

```yaml
passwords:
  stapp01: "Ir0nM@n"
  stapp02: "Am3ric@"
  stapp03: "BigGr33n"
```

Encrypt it using:

```bash
ansible-vault encrypt group_vars/application_servers/vault.yml
```

or simply by using : 
```bash
ansible-vault create group_vars/application_servers/vault.yml
```

Enter a secure password when prompted.

### 3. Creating the playbook file

### 4. Using Vault Password File for Seamless Execution

To avoid `--ask-vault-pass`, we created a **vault password file** to store the password created in **2**:

```bash
echo "YourVaultPassword" > ~/.ansible_vault_pass
chmod 600 ~/.ansible_vault_pass
```

Then, modify `ansible.cfg` to use it automatically:

```ini
[defaults]
vault_password_file = ~/.ansible_vault_pass
```

### 5. Running the Playbook

Run the playbook without extra arguments:

```bash
ansible-playbook -i inventory playbook.yml
```



---

**Note:** Always add `group_vars/application_servers/vault.yml` to `.gitignore` to prevent pushing sensitive data:

```bash
echo "group_vars/application_servers/vault.yml" >> .gitignore
git add .gitignore
git commit -m "Added .gitignore to protect secrets"
git push
```


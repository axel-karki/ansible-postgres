## PostgreSQL Setup (Ansible)

### What is PostgreSQL?

PostgreSQL is a powerful open-source relational database system. It supports advanced features like full-text search, JSON, and ACID compliance. It's widely used for web, data, and enterprise applications.

---

## What This Setup Does

This Ansible configuration installs and configures **PostgreSQL 17** on a Debian-based VM.

### Key Steps:

1. **Install Dependencies**: Installs required tools like `curl`, `sudo`, and `python3-psycopg2`.

2. **Add PostgreSQL APT Repo**:

   * Creates a directory for the GPG key.
   * Downloads and adds the official PostgreSQL repository based on the system codename.

3. **Install PostgreSQL 17**: Installs the database server and contrib package.

4. **Start and Enable Service**: Ensures PostgreSQL starts now and on boot.

5. **User and DB Creation**: Loads tasks from `users.yml` to create a superuser and application user with their database.

6. **Authentication Config**: Changes default local auth from `peer` to `md5` for password-based login.

7. **Restart Service**: Applies configuration changes.

8. **Access the database**:
   ```
   psql -U postgres -W
   ```
   Enter the password whem prompted.

---

## Secure Credentials with Ansible Vault

Variables like usernames and passwords in `vars/main.yml` should be encrypted.

### Vault Commands:

* Encrypt:

  ```bash
  ansible-vault encrypt vars/main.yml
  ```

* Edit:

  ```bash
  ansible-vault edit vars/main.yml
  ```

* Run playbook:

  ```bash
  ansible-playbook playbook.yml --ask-vault-pass
  ```

Or with password file:

```bash
ansible-playbook playbook.yml --vault-password-file ~/.vault_pass.txt
```

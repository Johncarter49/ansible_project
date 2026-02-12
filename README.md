# Prestashop + MySQL Ansible Project

This repository automates an e-commerce deployment scenario using two separate Ansible roles:

- `roles/mysql`: Installs and configures MySQL, enables external connectivity, and creates the Prestashop database and user.
- `roles/prestashop`: Installs Apache + PHP, downloads/extracts Prestashop files, and configures the Apache virtual host.

## Project structure

- `inventory.ini`: Target hosts (`db` and `web` groups)
- `site.yml`: Main playbook that orchestrates roles in order
- `roles/mysql/*`: Database role
- `roles/prestashop/*`: Web server role
- `requirements.yml`: Required Ansible collections
- `tests/test_results.txt`: Logs from executed checks

## How to run

1. Update host IPs and SSH users in `inventory.ini` for your environment.
2. Change default passwords in:
   - `roles/mysql/defaults/main.yml`
   - `roles/prestashop/defaults/main.yml`
3. Install required collection:
   ```bash
   ansible-galaxy collection install -r requirements.yml
   ```
4. Run syntax check:
   ```bash
   ansible-playbook --syntax-check site.yml
   ```
5. Launch deployment:
   ```bash
   ansible-playbook site.yml
   ```

## Notes

- Default HTTP port: `80`
- Default MySQL port: `3306`
- During Prestashop web installer, use:
  - DB host: your DB server IP
  - DB name: `prestashop`
  - DB user: `prestashop`
  - DB password: value of `mysql_prestashop_password`

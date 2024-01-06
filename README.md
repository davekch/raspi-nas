# NAS with samba
Ansible script to set up a simple NAS for a local network. Tested on a raspberry pi running Ubuntu server 22.04

## Setup
1. Set the host- and username of your raspberry pi in the `raspberries` section in `hosts.ini`
2. Install and setup [sops](https://github.com/getsops/sops). A basic `.sops.yaml` could look like this:
    ```yaml
    ---
    creation_rules:
        - pgp: KEY_FINGERPRINT
    ```
3. Create `vars.enc.yml` and fill it with your configuration, for example:
    ```yaml
    device: /dev/sdb1
    mountpoint: /mnt/sdb1
    shared_dir: /mnt/sdb1/shared
    nas_user: nas-user
    nas_password: nas-user-password
    become_pass: raspberry-root-password
    ```
4. Encrypt the secrets with sops: `sops -e -i vars.enc.yml`
5. Run the playbook: `ansible-playbook playbook.yml`

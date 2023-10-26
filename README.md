# Budgetbot Deployment Playbook

## About

This playbook is essential for deploying the infrastructure required for the production use of [Telegram Budgetbot](https://github.com/itsoneword/budgetbot).

## What It Does

- **Deploys a Wireguard Server:** Sets up a Wireguard VPN server and generates a client configuration, intended for the bot's author's personal usage.
- **Sets Up Webhook Server:** Deploys a [webhook server](https://github.com/adnanh/webhook) necessary for triggering redeployment on merges or commits to the repository.  
The webhook is linked to a bash script that handles bot redeployment.
- **Docker and Budgetbot Deployment:** Installs Docker and deploys the latest version of Budgetbot.

## How to Use

1. **Populate the Inventory File:** 
   - Add the IP address of your destination server to the `inventory.yml` file. 
   - Ensure the server is configured to accept SSH connections with a private key (without needing to specify the key via the `-i` parameter).
   - For more details, refer to the [Ansible Connection Guide](https://docs.ansible.com/ansible/latest/inventory_guide/connection_details.html).

   **Example:**
   ```yaml
   [server]
   192.168.0.10
2. **Configure Variables:**
   - Populate the variables in the vars folder for each task.
   - You can also use an encrypted vars file if you have the password (note: this is for internal use).

3. **Execute the Playbook:**  
   Run the following command to start the deployment:
     ```bash
     ansible-playbook server.yml -i inventory.yml
     ```
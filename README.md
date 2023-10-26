# Budgetbot Deployment Playbook

## About

This playbook is needed for deployment of a the infrastructure needed for production [telegram budgetbot](https://github.com/itsoneword/budgetbot) usage.  

## What does it do

 * Deploys a Wireguard server and generates a client configuration.  
 (for bot's author personal usage)

 * Deploys a [webhook](https://github.com/adnanh/webhook) server needed for triggering redeploy on merges/commits to the repository.  
 Webhook is connected to bash script which is responsible for bot redeployment.

 * Sets up docker, and deploys a recent version of budgetbot

 ## How to use it

 1) Create the `inventory` file containing an ip for a destination server.  
 (Make sure your server is configured to accept private to access a root account, and local ssh config file or SSH agent is set so when you connect to the server you don't need to specify this key using -i parameter). If you want to learn more, follow [Ansible docs](https://docs.ansible.com/ansible/latest/inventory_guide/connection_details.html).

 Example:
 ```
 [server]
192.168.0.10
 ```
2) Fill the variables in each task vars folder with your own.  
Or you can get them from encrypted vars file you have a password (you probably don't).

3) Start the playbook using
```
ansible-playbook server.yml -i inventory
```
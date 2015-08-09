Launching a Vagrant Local Stack:
================================

1.

> vagrant up

This will provision the vagrant stack with a management node that has ansible installed and configured.
the ssh keys then would need to be added in to each node after logging into this using the steps below.

2. create the ssh connections

> vagrant ssh mgmt

mgmt> ansible-playbook playbooks/ssh-addkey.yml --ask-pass
(enter vagrant as password)

3. get the site live

mgmt> ansible-playbook playbooks/site.yml

4. watch site running on http://localhost:8080/ and haproxy admin panel on http://localhost:8080/haproxy?stats

To repush the code run:

mgmt> ansible-playbook playbooks/deploy-webapp.yml

Launching the Stack in AWS:
===========================

Coming soon!
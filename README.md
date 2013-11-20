A file called 'vagrant_ansible_inventory_<machine-name>' is generated by
vagrant when the box is brought up, because the Vagrantfile does not refer to
an existing inventory file but something sensible can be figured out from the
other config.

To run arbitrary ansible commands on the Vagrant box, need specify Vagrant creds:

    ansible --user vagrant --sudo --private-key=~/.vagrant.d/insecure_private_key \
    -i vagrant_ansible_inventory_default all -m service -a "name=mysql state=restarted"

And the following are equivalent ways of provisioning the whole playbook on a running box:

    vagrant provision [--provision-with=ansible]

    ansible-playbook --user vagrant --sudo --private-key=~/.vagrant.d/insecure_private_key \
    -i vagrant_ansible_inventory_default azkaban-test.yml
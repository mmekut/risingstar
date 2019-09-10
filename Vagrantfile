##################################################
# Generated on phansible.com
# Curated by Mmekut
##################################################

Vagrant.configure("2") do |config|

    config.vm.define "ubuntu" do |u|
        
        u.vm.provider :virtualbox do |v|
            v.name = "Ubuntu-Cosmic"
            v.customize [
                "modifyvm", :id,
                "--name", "Cosmic",
                "--memory", 1024,
                "--natdnshostresolver1", "on",
                "--cpus", 1,
            ]
        end
        
        # Will download box from vagrant cloud...
        #...if it hasn't been downloaded manually
        u.vm.box = "bento/ubuntu-18.10"
        
        # Sets VM boot timeouts
        # Vagrant will timeout if VM takes longer than this value to
        # complete booting but you can still ssh into the machine after a while
        u.vm.boot_timeout = 600
    
        u.vm.network :private_network, ip: "192.168.56.10"
        u.ssh.forward_agent = true

        
        #Installs ansible locally and provisions inside the VM
        u.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "ansible/playbook.yml"
            ansible.inventory_path = "ansible/inventories/dev"
            ansible.galaxy_role_file = 'ansible/requirements.yml'
            
            ansible.galaxy_roles_path = '/vagrant/ansible/roles'
            ansible.galaxy_command = 'sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path}'
        end
        
        #syncronized folders in host and guest
        u.vm.synced_folder "projects", "/var/www/rising"
    end
end
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.boot_timeout = 0
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine
  end
  config.vm.define "audit" do |machine|
    machine.vm.hostname = "audit"
    machine.vm.provider "virtualbox" do |v|
      v.name = "Ansible CIS Bench - Audit"
    end
  end

  config.vm.provision "ansible_local", run: "always" do |ansible|
    ansible.playbook         = "setup.yml"
    ansible.playbook_command = "sudo ansible-playbook"
    ansible.install_mode     = "pip"
    ansible.pip_install_cmd  = "(until sudo apt update ; do sleep 1 ; done && sudo apt install -y python3-pip && sudo rm -f /usr/bin/pip && sudo ln -s /usr/bin/pip3 /usr/bin/pip && sudo -H pip install --upgrade pip) 2>&1 | sudo tee -a /var/log/vagrant-init"
  end
end

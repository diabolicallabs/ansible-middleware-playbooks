VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Use the same key for each machine
  config.ssh.insert_key = false
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end
  config.vm.define "vagrant1" do |vagrant1|
    vagrant1.vm.box = "centos/7"
    config.vm.synced_folder ".", "/home/vagrant/sync", disabled: true
    vagrant1.vm.network "forwarded_port", guest: 8080, host: 8080
    vagrant1.vm.network "forwarded_port", guest: 9990, host: 9990
    vagrant1.vm.network "forwarded_port", guest: 443, host: 8443

    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "bpms6.3-eap6.4-centos7-copy.yml"
      ansible.inventory_path = "inventory"
      ansible.sudo = true
    end
  end
end

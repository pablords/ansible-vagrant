
Vagrant.configure("2") do |config|

  config.vm.box_check_update = false
  config.ssh.insert_key = false
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end

  config.vm.define "centos" do |centos|
    centos.vm.box = "centos/8"
    centos.vm.network "private_network", ip: "192.168.50.11"
    centos.vm.provider "virtualbox" do |v|
      v.name = "centos"
    end
  end

  config.vm.define "debian" do |debian|
    debian.vm.box = "debian/jessie64"
    debian.vm.network "private_network", ip: "192.168.50.12"
    debian.vm.provider "virtualbox" do |v|
      v.name = "debian"
    end
  end

  config.vm.define "ubuntu", primary: true do |ubuntu|
    ubuntu.vm.box = "ubuntu/bionic64"
    ubuntu.vm.network "private_network", ip: "192.168.50.10"
    ubuntu.vm.synced_folder "./ansible", "/home/vagrant/ansible"
    ubuntu.vm.provider "virtualbox" do |v|
      v.name = "ubuntu"
      v.memory = 2048
      v.cpus = 2
    end
    ubuntu.vm.provision :ansible_local do |ansible|
        ansible.verbose           = true
        ansible.install           = true
        ansible.limit             = "all" # or only "nodes" group, etc.
        ansible.config_file       = "/home/vagrant/ansible/ansible.cfg"
        ansible.inventory_path    = "hosts"
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "playbook.yml"
    end
  end

end

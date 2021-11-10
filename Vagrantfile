
Vagrant.configure("2") do |config|

  config.ssh.insert_key = false

  config.vm.define "ubuntu", primary: true do |ubuntu|
    ubuntu.vm.box = "ubuntu/bionic64"
    ubuntu.vm.network "public_network", ip: "10.0.0.10", hostname: true
    ubuntu.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/id_rsa.pub"
    ubuntu.vm.provision :shell, :inline => "cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys", run: "always"
  end

  config.vm.define "centos" do |centos|
    centos.vm.box = "centos/7"
    centos.vm.network "public_network", ip: "10.0.0.15", hostname: true
    centos.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/id_rsa.pub"
    centos.vm.provision :shell, :inline => "cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys", run: "always"
  end

  config.vm.define "debian" do |debian|
    debian.vm.box = "debian/jessie64"
    debian.vm.network "public_network", ip: "10.0.0.16", hostname: true
    debian.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/id_rsa.pub"
    debian.vm.provision :shell, :inline => "cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys", run: "always"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
  end

end

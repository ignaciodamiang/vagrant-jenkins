Vagrant.configure("2") do |config|
  config.vm.define "master", primary: true do |master|
    master.vm.hostname = "master"
    master.vm.box = "ubuntu/jammy64"
    master.vm.network "private_network", ip: "192.168.56.4"
    master.vm.provision :shell, path: "master-bootstrap.sh"
    master.vm.network :forwarded_port, guest: 80, host: 8000
    master.vm.network :forwarded_port, guest: 8080, host: 8080
    master.vbguest.auto_update = false if Vagrant.has_plugin?("vagrant-vbguest")
    master.vm.provider "virtualbox" do |vbox1|
      vbox1.customize ["modifyvm", :id, "--memory", 2048]
      vbox1.customize ["modifyvm", :id, "--cpus", 2]
    end
  end
  config.vm.define "slave" do |slave|
    slave.vm.hostname = "slave"
    slave.vm.box = "ubuntu/jammy64"
    slave.vm.network "private_network", ip: "192.168.56.5"
    slave.vm.provision :shell, path: "slave-bootstrap.sh"
    slave.vbguest.auto_update = false if Vagrant.has_plugin?("vagrant-vbguest")
    slave.vm.provider "virtualbox" do |vbox2|
      vbox2.customize ["modifyvm", :id, "--memory", 1024]
      vbox2.customize ["modifyvm", :id, "--cpus", 1]
    end
  end
end
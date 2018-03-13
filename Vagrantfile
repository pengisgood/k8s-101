# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = false

  config.vm.network "private_network", ip: "192.168.10.10"
  config.vm.network "forwarded_port", guest: 30001, host: 30001, host_ip: "192.168.10.10"

  config.vm.synced_folder ".", "/home/vagrant/data"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "k8s-101-master"
    vb.cpus = "2"
    vb.memory = "1024"
  end
  
  config.vm.provision "shell", run: "always", inline: <<-SHELL
    sudo systemctl stop firewalld
    
    sudo yum install -y etcd kubernetes subscription-manager
    
    sudo systemctl start etcd
    sudo systemctl start docker
    sudo systemctl start kube-apiserver
    sudo systemctl start kube-controller-manager
    sudo systemctl start kube-scheduler
    sudo systemctl start kubelet
    sudo systemctl start kube-proxy
  SHELL
end

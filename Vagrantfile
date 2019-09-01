# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

    config.vm.box = "ubuntu/xenial64"
  
    config.vm.define "kube-01" do |kube|
      kube.vm.hostname = "kube-01"
      kube.vm.network "private_network", ip: "192.168.56.101"
      kube.vm.provider :virtualbox do |vb|
        vb.memory = 4096
        vb.cpus = 2
      end  
      kube.vm.provision "shell", inline: $script
    end
   
   config.vm.define "kube-02" do |kube|
      kube.vm.hostname = "kube-02"
      kube.vm.network "private_network", ip: "192.168.56.102"
      kube.vm.provider :virtualbox do |vb|
        vb.memory = 2048
        vb.cpus = 1
      end
      kube.vm.provision "shell", inline: $script
    end
  
   config.vm.define "kube-03" do |kube|
      kube.vm.hostname = "kube-03"
      kube.vm.network "private_network", ip: "192.168.56.103"
      kube.vm.provider :virtualbox do |vb|
         vb.memory = 2048
         vb.cpus = 1
      end
      kube.vm.provision "shell", inline: $script
    end
  
$script = <<SCRIPT
echo I am provisioning...
sudo cp /vagrant/hosts /etc/hosts
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo cp /vagrant/kubernetes.list /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update 
sudo apt-get install -y docker.io kubelet kubeadm kubectl kubernetes-cni
sudo rm -rf /var/lib/kubelet/*
echo I am turning off swap...
sudo swapoff -a
echo I am joining NFS...
sudo apt-get install nfs-common -y
SCRIPT
  
end
# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  # Kubernetes Master Server
  config.vm.define "master" do |kubemaster|
    kubemaster.vm.box = "centos/7"
    kubemaster.vm.hostname = "master.plb.form"
    kubemaster.vm.network "private_network", ip: "172.42.42.100"
    kubemaster.vm.provider "virtualbox" do |v|
      v.name = "master"
      v.memory = 2048
      v.cpus = 2
    end
    kubemaster.vm.provision "shell", path: "bootstrap.sh"
  end

  NodeCount = 2

  # Kubernetes Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "worker#{i}" do |workernode|
      workernode.vm.box = "centos/7"
      workernode.vm.hostname = "worker#{i}.plb.form"
      workernode.vm.network "private_network", ip: "172.42.42.10#{i}"
      workernode.vm.provider "virtualbox" do |v|
        v.name = "worker#{i}"
        v.memory = 1024
        v.cpus = 1
      end
      workernode.vm.provision "shell", path: "bootstrap.sh"
    end
  end

end

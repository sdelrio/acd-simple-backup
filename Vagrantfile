# -*- mode: ruby -*-
# vi: set ft=ruby :

$box = 'ubuntu/trusty64'
$box_url = nil
$box_version = nil
$backup_folder = 'D:\IMAGENES'
$vm_cores = 2
$vm_memory = 512

Vagrant.configure(2) do |config|

  config.vm.synced_folder ".", "/vagrant"
  config.vm.synced_folder $backup_folder, "/backup"

  config.vm.define "acd" do |d|

    # Machine name

    d.vm.hostname = "acd"

    # Base image configuration

    d.vm.box = $box
    d.vm.box_url = $box_url unless $box_url.nil?
    d.vm.box_version = $box_version unless $box_version.nil?

    # Provisioning with ansible on local

    d.vm.provision :shell, path: "scripts/bootstrap_ansible.sh"
    d.vm.provision :shell, inline: "PYTHONUNBUFFERED=1 ansible-playbook /vagrant/ansible/acd-cli.yml -c local"

    # Configure memory and cpu

    d.vm.provider "virtualbox" do |v|
      v.memory = $vm_memory
      v.cpus = $vm_cores
    end

  end

  # Enable cachier plugin if available (cache os packages)

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

end

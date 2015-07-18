# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network :private_network, ip: "192.168.50.2"
  config.vm.hostname = "ansible.loc"

  config.vm.synced_folder ".", "/opt/semaphore",
      type: "rsync",
      rsync__exclude: [".git", ".vagrant", "node_modules"],
      rsync__options: ["--verbose", "--archive", "--copy-links"]

  config.vm.provider "virtualbox" do |vb|
    # vb.gui = true
    vb.memory = 1024
    vb.cpus = 2
  end

  config.vm.provider :lxc do |lxc, override|
    override.vm.box = "trusty64-lxc"
    override.vm.box_url = "https://vagrantcloud.com/fgrehm/boxes/trusty64-lxc/versions/2/providers/lxc.box"
    lxc.backingstore = "btrfs"
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbooks/apache.yml"
    ansible.sudo = true
    ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
  end
end

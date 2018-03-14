# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV["LC_ALL"] = "en_US.UTF-8"

Vagrant.configure("2") do |config|
  config.vm.define "gcpx" do |gcpx|
    gcpx.vm.hostname = "gcpx"
    gcpx.vm.box = "debian/contrib-stretch64"
    gcpx.vm.network "private_network", type: "dhcp"
  end

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.name = "gcpx"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "sserver.yml"
    ansible.vault_password_file = "vault-pass"
    ansible.extra_vars = {
      "remote_user" => "vagrant",
      "vault_common_sshd_port" => "22",
      "vault_mosh_port_range" => "60000:61000"
    }
    ansible.groups = {
      "fqservers" => ["gcpx"]
    }
  end
end

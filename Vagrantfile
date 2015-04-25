# -*- mode: ruby -*-
# vi: set ft=ruby :

defaultbox = "chef/centos-6.5"
box = ENV['BOX'] || defaultbox

ENV['ANSIBLE_ROLES_PATH'] = "../../roles"

Vagrant.configure(2) do |config|

  config.vm.box = box
  
  config.vm.define "nginx" do |nginx_cfg|
    nginx_cfg.vm.network :forwarded_port, host: 8081, guest: 80
    nginx_cfg.vm.provider :virtualbox do |v|
      v.name = "nginx"
      # v.gui = true
    end
  end
  
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "example/nginx.yml"
    ansible.sudo = true
    # ansible.tags = ['debug']
    ansible.extra_vars = {
      ansible_ssh_user: 'vagrant',
      hbase_standalone: true,
    }

  end

end

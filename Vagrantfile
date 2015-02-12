# -*- mode: ruby -*-
# vi: set ft=ruby :

defaultbox = "centos65-x86_64-20140116"
box = ENV['BOX'] || defaultbox

ENV['ANSIBLE_ROLES_PATH'] = "../../roles"

Vagrant.configure(2) do |config|

  config.vm.box = box
  if box == defaultbox
      config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"
  end
  
  config.vm.define "nginx" do |nginx_cfg|
    nginx_cfg.vm.network :forwarded_port, host: 8080, guest: 80
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

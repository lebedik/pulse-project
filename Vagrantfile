# -*- mode: ruby -*-
# vi: set ft=ruby :
GLOBAL_BOX = "xanagi/centos-6.5-chef"
GLOBAL_CONFIG = {
  "mysql" => {
    "server_debian_password" => "123456",
    "server_root_password" => "123456",
    "server_repl_password" => "123456",
  },
    'pulse' => {
      'db_host' => '192.168.33.112'
    }
  }
Vagrant.configure(2) do |config|
  config.omnibus.chef_version = '12.8.1'
  config.vm.define 'db' do |db|
    db.vm.box = GLOBAL_BOX
    db.vm.network "private_network", ip: "192.168.33.112"
     db.vm.provider "virtualbox" do |vb|
       vb.memory = "512"
     end
    db.vm.provision "chef_solo" do |chef|
      chef.cookbooks_path = ["chef/cookbooks"]
      chef.roles_path = "chef/roles"
      chef.add_recipe "pulse::db-server"
      chef.json = GLOBAL_CONFIG
    end
  end
end

Vagrant.configure(2) do |config|
  config.omnibus.chef_version = '12.8.1'
  config.vm.define 'app' do |app|
    app.vm.box = GLOBAL_BOX
    app.vm.network "private_network", ip: "192.168.33.111"
     app.vm.provider "virtualbox" do |vb|
       vb.memory = "1024"
     end
    app.vm.provision "chef_solo" do |chef|
      chef.cookbooks_path = ["chef/cookbooks"]
      chef.roles_path = "chef/roles"
      chef.add_recipe "pulse::app-server"
      chef.json = GLOBAL_CONFIG
    end
  end
end

Vagrant.configure(2) do |config|
  config.omnibus.chef_version = '12.8.1'
  config.vm.define 'web' do |web|
    web.vm.box = GLOBAL_BOX
    web.vm.network "private_network", ip: "192.168.33.113"
     web.vm.provider "virtualbox" do |vb|
       vb.memory = "256"
     end
    web.vm.provision "chef_solo" do |chef|
      chef.cookbooks_path = ["chef/cookbooks"]
      chef.roles_path = "chef/roles"
      chef.add_recipe "pulse::web-server"
      chef.json = GLOBAL_CONFIG
    end
  end
end


Vagrant.configure(2) do |config|
  config.omnibus.chef_version = '12.8.1'
  config.vm.define 'zbx' do |zbx|
    zbx.vm.box = GLOBAL_BOX
    zbx.vm.network "private_network", ip: "192.168.33.200"
     zbx.vm.provider "virtualbox" do |vb|
       vb.memory = "256"
     end

    zbx.vm.provision "chef_solo" do |chef|
      chef.cookbooks_path = ["chef/cookbooks"]
      chef.roles_path = "chef/roles"
      chef.add_role "zabbix-srv"
      chef.json = GLOBAL_CONFIG
    end
  end
end

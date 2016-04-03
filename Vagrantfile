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
      'db_host' => '192.168.33.112', 
      'jmx_host' => '192.168.33.111'
    },

    "epc-provisioning": {
    "instances": {
      "zbx.budapest.epam.com": {
        "private_ip_address": "192.168.33.200",
        "description": "zabbix_srv",
        "name": "zbx.epplkraw0175t1",
        "id": "i-f1ad2948",
        "run_list": [
          "role[zabbix-srv]"
        ],
        "role": "zabbix-srv"
      },
      "db.budapest.epam.com": {
        "private_ip_address": "192.168.33.112",
        "description": "db_bundle",
        "name": "db.epplkraw0175t1",
        "id": "i-9ce1882c",
        "run_list": [
          "role[db-bundle]"
        ],
        "role": "db-bundle"
      },
       "web.budapest.epam.com": {
        "private_ip_address": "192.168.33.113",
        "description": "WEB_bundle",
        "name": "web.epplkraw0175t1",
        "id": "i-9ce1882F",
        "run_list": [
          "role[web-bundle]"
        ],
        "role": "web-bundle"
      },
      "app.budapest.epam.com": {
        "private_ip_address": "192.168.33.111",
        "description": "app_bundle",
        "name": "app.epplkraw0175t1",
        "id": "i-9ce1882a",
        "run_list": [
          "role[app-bundle]"
        ],
        "role": "app-bundle"
      }
    }
}
  }
Vagrant.configure(2) do |config|
  config.omnibus.chef_version = '12.8.1'
  config.vm.define 'db' do |db|
    db.vm.box = GLOBAL_BOX
    db.vm.hostname = "db.budapest.epam.com"
    db.vm.network "private_network", ip: "192.168.33.112"
     db.vm.provider "virtualbox" do |vb|
       vb.memory = "512"
     end
    db.vm.provision "chef_solo" do |chef|
      chef.cookbooks_path = ["chef/cookbooks"]
      chef.roles_path = "chef/roles"
      chef.add_role("db-server")
      chef.json = GLOBAL_CONFIG
    end
  end
end

Vagrant.configure(2) do |config|
  config.omnibus.chef_version = '12.8.1'
  config.vm.define 'app' do |app|
    app.vm.box = GLOBAL_BOX
    app.vm.hostname = "app.budapest.epam.com"
    app.vm.network "private_network", ip: "192.168.33.111"
     app.vm.provider "virtualbox" do |vb|
       vb.memory = "1024"
     end
    app.vm.provision "chef_solo" do |chef|
      chef.cookbooks_path = ["chef/cookbooks"]
      chef.roles_path = "chef/roles"
      chef.add_role("app-server")
      chef.json = GLOBAL_CONFIG
    end
  end
end

Vagrant.configure(2) do |config|
  config.omnibus.chef_version = '12.8.1'
  config.vm.define 'web' do |web|
    web.vm.box = GLOBAL_BOX
    web.vm.network "private_network", ip: "192.168.33.113"
    web.vm.hostname = "web.budapest.epam.com"
     web.vm.provider "virtualbox" do |vb|
       vb.memory = "256"
     end
    web.vm.provision "chef_solo" do |chef|
      chef.cookbooks_path = ["chef/cookbooks"]
      chef.roles_path = "chef/roles"
      chef.add_role("web-server")
      chef.json = GLOBAL_CONFIG
    end
  end
end


Vagrant.configure(2) do |config|
  config.omnibus.chef_version = '12.8.1'
  config.vm.define 'zbx' do |zbx|
    zbx.vm.box = GLOBAL_BOX
    zbx.vm.hostname = "zbx.budapest.epam.com"
    zbx.vm.network "private_network", ip: "192.168.33.200"
     zbx.vm.provider "virtualbox" do |vb|
       vb.memory = "256"
     end

    zbx.vm.provision "chef_solo" do |chef|
      chef.cookbooks_path = ["chef/cookbooks"]
      chef.roles_path = "chef/roles"
      chef.add_role("zabbix-srv")
      chef.json = GLOBAL_CONFIG
    end
  end
end

# -*- mode: ruby -*-
Vagrant.configure(2) do |config|
  config.vm.box = 'centos/7'

  config.vm.network :forwarded_port, guest: 80, host: 8080

  config.vm.provider 'virtualbox' do |vb|
    vb.memory = '1024'
    vb.cpus = 2
  end

  config.vm.provision :chef_client do |chef|
    chef.chef_server_url = 'https://api.opscode.com/organizations/jhdc'
    chef.validation_key_path = "#{ENV['HOME']}/.chef/jhdc-validator.pem"
    chef.validation_client_name = 'jhdc-validator'
    chef.node_name = 'jhdc-staging'
    chef.environment = 'staging'
    chef.delete_node = true
    chef.delete_client = true
    chef.run_list = ['jhdc-base', 'jhdc-web']
    chef.json = { authorization: { sudo: {
      groups: ['sysadmin'],
      users: ['vagrant'],
      passwordless: true } } }
  end
end

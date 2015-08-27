Vagrant.configure('2') do |config|

    # Global settings
    require 'yaml'
    current_dir = File.dirname(File.expand_path(__FILE__))
    configs = YAML.load_file("#{current_dir}/config.yaml")
    vagrant_config = configs['configs'][configs['configs']['use']]

    # SSH Configuration
    config.ssh.username = 'root'
    config.ssh.private_key_path = '~/.ssh/id_rsa'

    # Linode configuration
    config.vm.provider :linode do |provider, override|
        override.vm.box = 'linode'
        override.vm.box_url = "https://github.com/displague/vagrant-linode/raw/master/box/linode.box"
        provider.token = vagrant_config['token']

        # Node settings
        provider.distribution = vagrant_config['distribution']
        provider.datacenter = vagrant_config['datacenter']
        provider.plan = vagrant_config['plan']
        provider.label = vagrant_config['label']
    end

    #Chef Configuration
    config.vm.provision :chef_solo do |chef|
        chef.add_recipe "database"
    end
end

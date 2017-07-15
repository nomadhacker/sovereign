# -*- mode: ruby -*-

Vagrant.configure('2') do |config|
  config.vm.hostname = 'sovereign.local'
  config.vm.network 'private_network', ip: '172.16.100.2'

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'site.yml'
    ansible.host_key_checking = false
    ansible.verbose = true
    ansible.extra_vars = { ansible_ssh_user: 'vagrant', testing: true }
    ansible.groups = {
      "testing" => ["stretch"]
    }

    # ansible.tags = ['blog']
    # ansible.skip_tags = ['openvpn']
    # ansible.verbose = 'vvvv'
  end

  config.vm.provider :virtualbox do |v|
    v.memory = 512
  end

  config.vm.provider :vmware_fusion do |v|
    v.vmx['memsize'] = '512'
  end

  # vagrant-cachier
  #
  # Install the plugin by running: vagrant plugin install vagrant-cachier
  # More information: https://github.com/fgrehm/vagrant-cachier
  if Vagrant.has_plugin? 'vagrant-cachier'
    config.cache.enable :apt
    config.cache.scope = :box
  end

  # Debian 9 64-bit (officially supported)
  config.vm.define 'stretch', primary: true do |stretch|
    stretch.vm.box = 'debian/stretch64'
  end

  # Debian 8 64-bit (officially supported)
  config.vm.define 'jessie', autostart: false do |jessie|
    jessie.vm.box = 'box-cutter/debian8'
  end

  # Ubuntu 16.04 (LTS) 64-bit (currently unavailable)
  config.vm.define 'xenial', autostart: false do |xenial|
    xenial.vm.box = 'box-cutter/ubuntu1604'
  end
end

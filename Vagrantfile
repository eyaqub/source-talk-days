# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

env_config = {
   :memory       => 1024,
   :box          => {:name => "ubuntu-13.04", :url => "http://wwwuser.gwdg.de/~pkasprz/puppet-devel-ubuntu-13.04.box"},
   :hostname     => "talk.gwdg.de",
   :port_forward => [
      {guest: 80, host: 8080}
   ],
}

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
   # General virtualbox settings
   config.vm.provider :virtualbox do |vb|
#     vb.gui = true
   end
   
   config.vm.hostname  = env_config[:hostname]
   config.vm.box       = env_config[:box][:name]
   config.vm.box_url   = env_config[:box][:url]

   config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory",  env_config[:memory]]
   end

   # Define networks
   config.vm.network :private_network, ip: '10.1.1.3', netmask: '255.255.255.0', auto_config: true
                
   # Define portforwarding
   unless env_config[:port_forward].nil?
      env_config[:port_forward].each do |port_forward_config|
         config.vm.network :forwarded_port, guest: port_forward_config[:guest], host: port_forward_config[:host]
      end
   end

  #config.vm.provision :shell do |s|
  #  s.inline = 'puppet module install puppetlabs/vcsrepo'
  #end

  config.vm.provision :shell, path: "./scripts/script.sh"

   # Enable puppet provisioning
  #config.vm.provision :puppet do |puppet|
  #   puppet.options = "--verbose --debug"
  #   puppet.module_path = "puppet/modules"
  #   puppet.manifests_path = "puppet/manifest"
  #   puppet.manifest_file  = "site.pp"
  #end

end



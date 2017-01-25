# -*- mode: ruby -*-
# vi: set ft=ruby :


# Make sure shared folders exist
FileUtils.mkdir_p(File.dirname(__FILE__)+'/sites')
FileUtils.mkdir_p(File.dirname(__FILE__)+'/sites/000-default')
FileUtils.mkdir_p(File.dirname(__FILE__)+'/sites/000-template')
FileUtils.mkdir_p(File.dirname(__FILE__)+'/logs')

# Set vagrant directory
vagrant_dir = File.expand_path(File.dirname(__FILE__))

Vagrant.configure("2") do |config|

	# Vagrant verison
	vagrant_version = Vagrant::VERSION.sub(/^v/, '')

	# Default box
	config.vm.box = "boxcutter/ubuntu1604"
	
	# IP - private network only
	config.vm.network :private_network, id: "apollo_primary", ip: "10.10.10.10"
	
	# Hostname
	config.vm.hostname = "apollo"
	config.ssh.forward_agent = true

	# This supresses the harmless but annoying 'stdin: is not a tty' error that is generated every time a shell script provisioner is run
	config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

	# Synced folders	
	if vagrant_version >= "1.3.0"
		config.vm.synced_folder "logs", "/projects/logs", owner: "vagrant", group: "www-data"
                config.vm.synced_folder "sites", "/projects/sites", owner: "vagrant", group: "www-data"
	else
		config.vm.synced_folder "logs", "/projects/logs", :owner => "vagrant"
		config.vm.synced_folder "sites", "/projects/sites", :owner => "vagrant"
	end

	# Provisioning script
	config.vm.provision "shell", path: ".config/apollo-setup.sh"

	# Restart services on boot
	if vagrant_version >= "1.6.0"
		config.vm.provision :shell, inline: "sudo service mysql restart", run: "always"
		config.vm.provision :shell, inline: "sudo service nginx restart", run: "always"
		config.vm.provision :shell, inline: "sudo service php7.0-fpm restart", run: "always"
	end

	# Prefer VMware Fusion before VirtualBox
	config.vm.provider "vmware_fusion"
	config.vm.provider "virtualbox"

	# VM Ware specific configuration
	config.vm.provider "vmware_fusion" do |v|
		v.vmx["memsize"] = "2048"
		v.vmx["numvcpus"] = "2"
	end

	# Virtualbox specific configuration
	config.vm.provider "virtualbox" do |v|
		v.customize ["modifyvm", :id, "--memory", 2048]
		v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
	end


	# Load Customfile if it exists
	if File.exists?(File.join(vagrant_dir,'Customfile')) then
		eval(IO.read(File.join(vagrant_dir,'Customfile')), binding)
	end

end

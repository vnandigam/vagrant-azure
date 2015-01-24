# -*- mode: ruby -*-
# vi: set ft=ruby :
ENV['VAGRANT_DEFAULT_PROVIDER'] ||= 'azure'
 
Vagrant.configure("2") do |config|	

config.vm.box = 'azure'

    config.vm.provider :azure do |azure|
        azure.mgmt_certificate = ‘PATH_TO_CERT.pem'
        azure.mgmt_endpoint = 'https://management.core.windows.net'
        azure.subscription_id = ‘XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX’
        azure.storage_acct_name = 'vivovagrant' # optional. A new one will be generated if not provided.

        azure.vm_image = 'b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-12_04_4-LTS-amd64-server-20140428-en-us-30GB'
        azure.vm_user = 'vagrant' # Using 'vagrant' as username overcame some of the hardcoding issues in the installer
        azure.vm_password = ’SET_PASSWORD’ # min 8 characters. should contain a lower case letter, an uppercase letter, a number and a special character

        azure.vm_name = 'vivovagrantVM’ # max 15 characters. contains letters, number and hyphens. can start with letters and can end with letters and numbers
        azure.cloud_service_name = 'vivovagrantVM’ # same as vm_name. leave blank to auto-generate
        azure.deployment_name = 'vivovagrantVM’ # defaults to cloud_service_name
        azure.vm_location = 'West US' # e.g., West US
        azure.vm_size = 'Small' 
        azure.ssh_private_key_file = ‘PATH_TO_KEY.key'
        azure.ssh_certificate_file = ‘PATH_TO_CERT.cer'

        # Provide the following values if creating a *Nix VM
        
		azure.ssh_port = '22'
		azure.tcp_endpoints = '8080:8080' 
        
        # Provide the following values if creating a Windows VM
        #azure.winrm_transport = [ 'http', 'https' ] # this will open up winrm ports on both http (5985) and http (5986) ports
        #azure.winrm_https_port = 'A VALID PUBLIC PORT' # customize the winrm https port, instead of 5986
        #azure.winrm_http_port = 'A VALID PUBLIC PORT' # customize the winrm http port, insted of 5985
        #azure.tcp_endpoints = '3389:53389' # opens the Remote Desktop internal port that listens on public port 53389. Without this, you cannot RDP to a Windows VM.
    end

	config.ssh.username = 'vagrant' # the one used to create the VM
	config.ssh.password = ‘SET_PASSWORD’ # the one used to create the VM

	# Forward a port from the guest to the host, which allows for outside
	# computers to access the VM, whereas host only networking does not.
	
	config.vm.network "forwarded_port", guest: 80, host: 8081
	config.vm.network "forwarded_port", guest: 8080, host: 8080
	config.vm.network "forwarded_port", guest: 8000, host: 8000
	config.vm.network "forwarded_port", guest: 5000, host: 5000
	config.vm.network "forwarded_port", guest: 3030, host: 3030

	# Share an additional folder to the guest VM. The first argument is
	# an identifier, the second is the path on the guest to mount the
	# folder, and the third is the path on the host to the actual folder.
	
	config.vm.synced_folder "work", "/work"
	config.vm.synced_folder "provision", "/home/vagrant/provision"  
	config.vm.provision "shell", path: "provision/bootstrap.sh", privileged: true	
end

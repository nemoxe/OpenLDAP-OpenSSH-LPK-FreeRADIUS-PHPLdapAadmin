vms = [

{:hostname => 'openldap.truss.com', :ip => '10.127.0.10', :box => 'ubuntu/trusty64', :ram => 1024, :cpus => 1,},
{:hostname => 'nodo1.truss.com', :ip => '10.127.0.200', :box => 'ubuntu/trusty64', :ram => 1024, :cpus => 1,},
]

Vagrant.configure("2") do |config|
	vms.each do |create_vm|
		config.vm.define create_vm[:hostname] do |vm_config|
			vm_config.vm.box = create_vm[:box]
			vm_config.vm.hostname = create_vm[:hostname]
			vm_config.vm.network :private_network, ip: create_vm[:ip]
			memory = create_vm[:ram] ? create_vm[:ram] : 256;
			cpu = create_vm[:cpus] ? create_vm[:cpus] : 1;
			vm_config.vm.provider :virtualbox do |cust|
				cust.customize [
					'modifyvm', :id,
					'--name', create_vm[:hostname],
					'--memory', memory.to_s,
					'--cpus', cpu.to_s
						]
			end

			vm_config.vm.provision :shell, :inline => "apt-get update --fix-missing"

		end
	end
end

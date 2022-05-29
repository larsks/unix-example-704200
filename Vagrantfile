# vim: set ft=ruby:

Vagrant.configure("2") do |config|
  config.vm.provider :libvirt do |libvirt|
    libvirt.uri = "qemu:///system"
    libvirt.memory = 4096
  end

  config.vm.box = "fedora/36-cloud-base"
  config.vm.box_version = "36-20220504.1"


  config.vm.define "router" do |router|
    router.vm.hostname = "router"
    router.vm.provider :libvirt do |libvirt|
      libvirt.storage :file,
        :size => "10G",
        :type => "qcow2"
    end

    router.vm.network :private_network,
      :libvirt__network_name => "lan0",
      :libvirt__forward_mode => "veryisolated",
      :libvirt__dhcp_enabled => false

    router.vm.network :private_network,
      :libvirt__network_name => "lan1",
      :libvirt__forward_mode => "veryisolated",
      :libvirt__dhcp_enabled => false

    router.vm.network :private_network,
      :libvirt__network_name => "lan2",
      :libvirt__forward_mode => "veryisolated",
      :libvirt__dhcp_enabled => false
  end

  config.vm.define "server" do |server|
    server.vm.hostname = "server"
    server.vm.provider :libvirt do |libvirt|
      libvirt.storage :file,
        :size => "10G",
        :type => "qcow2"
    end

    server.vm.network :private_network,
      :libvirt__network_name => "lan0",
      :libvirt__forward_mode => "veryisolated",
      :libvirt__dhcp_enabled => false
  end

  config.vm.define "client" do |client|
    client.vm.hostname = "client"
    client.vm.provider :libvirt do |libvirt|
      libvirt.storage :file,
        :size => "10G",
        :type => "qcow2"
    end

    client.vm.network :private_network,
      :libvirt__network_name => "lan1",
      :libvirt__forward_mode => "veryisolated",
      :libvirt__dhcp_enabled => false
  end

  config.vm.provision :ansible do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "provision/all.yaml"
    ansible.galaxy_role_file = "provision/requirements.yaml"
    ansible.host_vars = {
      "client" => {
        "ip_address": "10.133.7.100/24"
      },
      "server" => {
        "ip_address": "10.133.8.11/24"
      }
    }
  end

end

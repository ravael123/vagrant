# vagrant
repositori untuk belajar vagrant
Vagrant.configure("2") do |config|
      config.vm.box = "generic/alpine318"
      config.vm.network "public_network", type: "dhcp"
      config.vm.hostname "server1"

      machine.vm.provider "virtualbox" do |vb|
        vb.memory = "512"
        vb.cpus = "1"
        vb.name = "server1"
      end
      
    config.vm.provision "shell", inline: <<-SHELL
      apk update
      apk add apache2
      service apache2 start
      SHELL
end

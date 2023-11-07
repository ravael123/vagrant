Vagrant.configure("2") do |config|
  (1..2).each do |i|
    config.vm.define "vm#{i}" do |vm|
      vm.vm.box = "generic/alpine318"
      vm.vm.hostname = "charles-vm#{i}"
      vm.vm.network "private_network", type: "dhcp"
      vm.vm.provider "virtualbox" do |vb|
        vb.memory = "512"
        vb.cpus = 1
        vb.name = "my-vm#{i}"  # Menambahkan pengaturan vb.name
      end

      package_name = i == 1 ? "apache2" : "nginx"
      vm.vm.provision "shell", inline: <<-SHELL
        apk update
        apk add #{package_name}
        service #{package_name} start
      SHELL
    end
  end
end

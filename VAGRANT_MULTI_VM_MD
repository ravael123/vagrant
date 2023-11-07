Vagrant.configure("2") do |config|
  # Konfigurasi VM pertama
  config.vm.define "vm1" do |vm1|
    vm1.vm.box = "generic/alpine318"
    vm1.vm.hostname = "charles-vm1"
    vm1.vm.network "public_network"
    
    vm1.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 1
      vb.name = "latihan-asj2-vm1"
    end

    vm1.vm.provision "shell", inline: <<-SHELL
      apk update
      apk add apache2
      service apache2 start
    SHELL
  end

  # Konfigurasi VM kedua
  config.vm.define "vm2" do |vm2|
    vm2.vm.box = "generic/alpine318"
    vm2.vm.hostname = "charles-vm2"
    vm2.vm.network "public_network"
    
    vm2.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = 1
      vb.name = "latihan-asj2-vm2"
    end

    vm2.vm.provision "shell", inline: <<-SHELL
      apk update
      apk add nginx
      service nginx start
    SHELL
  end
end

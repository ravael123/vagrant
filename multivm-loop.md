Vagrant.configure("2") do |config|
  # Daftar VM yang akan dibuat
  vms = [
    { name: "vm1", box: "generic/alpine318", hostname: "charles-vm1", provision_command: "apk add apache2; service apache2 start" },
    { name: "vm2", box: "generic/alpine318", hostname: "charles-vm2", provision_command: "apk add nginx; service nginx start" }
  ]

  # Loop untuk membuat dan mengonfigurasi setiap VM
  vms.each do |vm|
    config.vm.define vm[:name] do |node|
      node.vm.box = vm[:box]
      node.vm.hostname = vm[:hostname]
      node.vm.network "public_network"

      node.vm.provider "virtualbox" do |vb|
        vb.memory = "512"
        vb.cpus = 1
        vb.name = "latihan-asj2-#{vm[:name]}"
      end

      node.vm.provision "shell", inline: <<-SHELL
        apk update
        #{vm[:provision_command]}
      SHELL
    end
  end
end

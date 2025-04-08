Vagrant.configure("2") do |config|
  # Configuración del nodo manager
  config.vm.define "manager" do |manager|
    manager.vm.box = "bento/ubuntu-22.04"
    manager.vm.hostname = "swarm-manager"
    manager.vm.network "private_network", ip: "192.168.33.10"
    manager.vm.network "forwarded_port", guest: 80, host: 8080 # Acceso a la app en el manager
    manager.vm.provision "shell", inline: <<-SHELL
      # Instalar Docker según procedimientos oficiales
      curl -fsSL https://get.docker.com -o get-docker.sh
      sudo sh get-docker.sh
      sudo usermod -aG docker vagrant
      newgrp docker # Aplicar los cambios de grupo inmediatamente
    SHELL
    manager.vm.synced_folder ".", "/vagrant"
  end

  # Configuración del nodo worker (nodo1)
  config.vm.define "nodo1" do |nodo1|
    nodo1.vm.box = "bento/ubuntu-22.04"
    nodo1.vm.hostname = "swarm-nodo1"
    nodo1.vm.network "private_network", ip: "192.168.33.11" # Diferente IP para el nodo
    # No es necesario exponer puertos de la aplicación directamente en el worker
    nodo1.vm.provision "shell", inline: <<-SHELL
      # Instalar Docker según procedimientos oficiales
      curl -fsSL https://get.docker.com -o get-docker.sh
      sudo sh get-docker.sh
      sudo usermod -aG docker vagrant
      newgrp docker # Aplicar los cambios de grupo inmediatamente
    SHELL
    nodo1.vm.synced_folder ".", "/vagrant"
  end
end
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-24.04"
  config.ssh.insert_key = false

  config.vm.define "haproxy" do |h|
    h.vm.hostname = "haproxy-balancer"
    h.vm.network "private_network", ip: "192.168.56.50"

    # Провижининг: установка HAProxy + Python
    h.vm.provision "shell", inline: <<-SHELL
      export DEBIAN_FRONTEND=noninteractive
      apt-get update

      # Установка HAProxy и Python
      apt-get install -y haproxy python3 curl

      # Включаем HAProxy (по умолчанию выключен)
      sed -i 's/ENABLED=0/ENABLED=1/' /etc/default/haproxy

      # Создаём директорию для конфигов
      mkdir -p /vagrant/configs
    SHELL
  end
end

# config.vm.provision "shell", inline: <<-SHELL
#   export DEBIAN_FRONTEND=noninteractive
#   apt-get update
#   apt-get install -y nginx haproxy vim curl python3
#   sed -i 's/ENABLED=0/ENABLED=1/' /etc/default/haproxy
#   systemctl enable --now nginx haproxy
# SHELL

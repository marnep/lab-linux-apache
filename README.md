# 💻 Projeto IaC Local com Vagrant: VM Ubuntu com Apache

Este repositório contém um exemplo prático de Infraestrutura como Código (IaC) usando Vagrant para criar uma VM Ubuntu 18.04 LTS com Apache instalado automaticamente.

## 📦 Pré-requisitos
- [Git](https://git-scm.com/download/win)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant](https://developer.hashicorp.com/vagrant/downloads)
- [Visual Studio Code](https://code.visualstudio.com/)

## 📁 Estrutura do Projeto
```
lab-linux-apache/
└── Vagrantfile
```

## ⚙️ Conteúdo do `Vagrantfile`
```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.hostname = "webserver"
  config.vm.network "private_network", ip: "192.168.56.10"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 1
  end

  config.vm.provision "shell", inline: <<-SHELL
    echo "[INFO] Atualizando pacotes..."
    sudo apt update
    sudo apt install -y apache2
    sudo systemctl enable apache2
    sudo systemctl start apache2
    echo "[INFO] Apache instalado e iniciado com sucesso!"
  SHELL
end
```

## 🚀 Como executar
```powershell
cd C:\labs\lab-linux-apache
vagrant up
```
Acesse no navegador: [http://192.168.56.10](http://192.168.56.10)

## 🛠️ Comandos úteis
```bash
vagrant ssh         # Acessar a VM
vagrant halt        # Desligar a VM
vagrant reload      # Reiniciar a VM
vagrant destroy -f  # Apagar a VM
```

## 📌 Observações
- Este provisionamento usa shell script.
- O Ansible pode ser integrado nas próximas etapas via WSL.

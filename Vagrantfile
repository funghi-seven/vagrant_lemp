# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # latestのCentOSを指定（今だと6.9）
	config.vm.box = "centos/6"

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.enabled  = true
    config.proxy.no_proxy = "localhost,127.0.0.1"
  end

  if Vagrant.has_plugin?("vagrant-vbguest")
    # vagramt-vbguestをアップデート
    config.vbguest.auto_update = true
  end

  # Vagrant標準設定。理由がなければそのままでOK
  config.vm.network "private_network", ip: "192.168.33.30"
  # publicはあんまり使わない
  #config.vm.network :public_network, bridge: "en0: Ethernet"

  # insecure_keyを差し替えないようにする
  config.ssh.insert_key = false

  # ansible
  config.vm.synced_folder "./ansible/", "/tmp/ansible/", owner: "vagrant", group: "vagrant"

  config.vm.provider :virtualbox do |vb|
    # GUI mode off
    vb.gui = false
    # Memory 512MB, CPU 1core
    vb.customize ["modifyvm", :id, "--memory", "512", "--cpus", "1", "--ioapic", "on"]

    # ネットワークが遅くなるのを防ぐ
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
  end

  # yum updateする
  config.vm.provision "shell", inline:
  <<-SHELL
    sudo yum -y update
  SHELL

  # ansible_local provisioning
  config.vm.provision "ansible_local" do |ansible|
    ansible.limit = "all"
    ansible.playbook = "/tmp/ansible/playbook.yml"
  end

end

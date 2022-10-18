Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vagrant.plugins = "vagrant-reload"

  config.vm.provider "virtualbox" do |vb|    
    vb.cpus = 2
    vb.memory = 4096
    vb.gui = true
    vb.customize ['modifyvm', :id, '--clipboard-mode', 'bidirectional']
    vb.customize ['modifyvm', :id, '--draganddrop', 'bidirectional']
    vb.customize ["modifyvm", :id, "--vram", "128"]
  end

  config.vm.synced_folder ".", "/home/vagrant/Desktop/badass", type: "virtualbox"
  config.vm.provision "shell", name: "Setting up VM", privileged: false,  inline: <<-SHELL
    set -ex
    sudo add-apt-repository -y ppa:gns3/ppa
    sudo apt-get update
    DEBIAN_FRONTEND=noninteractive sudo apt-get install -y --no-install-recommends gdm3 ubuntu-desktop-minimal
    echo "display manager and desktop installed."
    

    gsettings set org.gnome.shell favorite-apps "$(gsettings get org.gnome.shell favorite-apps | sed s/.$//), 'org.gnome.Terminal.desktop']"
    echo "gns3, wireskark and terminal added to favorites."
  SHELL

  config.vm.provision :reload

  config.vm.provision "shell", name: "Setting up badass", privileged: false,  inline: <<-SHELL
    cd ~/Desktop/badass/requirements
    sudo docker build -f ./Dockerfile.router -t badass.router ./
    sudo docker pull alpine:3.16

    # old one
    # sudo docker build -f ./Dockerfile.router -t routeur_niduches ./
    # docker pull alpine
    # docker tag alpine:3.16 host_niduches
  SHELL

end

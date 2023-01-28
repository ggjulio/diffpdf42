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

  config.vm.synced_folder ".", "/home/vagrant/Desktop/pdf_files", type: "virtualbox"
  config.vm.provision "shell", name: "Setting up VM", privileged: false,  inline: <<-SHELL
    set -ex
    sudo apt-get update
    DEBIAN_FRONTEND=noninteractive sudo apt-get install -y --no-install-recommends ubuntu-desktop-minimal
    echo "display manager and desktop installed."
    
    sudo apt-get install -y diffpdf

    gsettings set org.gnome.shell favorite-apps "$(gsettings get org.gnome.shell favorite-apps | sed s/.$//), 'org.gnome.Terminal.desktop', 'diffpdf.desktop']"
    echo "terminal and diffpdf added to favorites."
  SHELL

  config.vm.provision :reload

  config.vm.provision "shell", name: "Setting up ", privileged: false,  inline: <<-SHELL
    echo ok
  SHELL

end

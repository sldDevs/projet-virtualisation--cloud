Vagrant.configure("2") do |config|
  # Utilisation d'une image Ubuntu standard pour VMware
  config.vm.box = "bento/ubuntu-22.04"

  # --- CONFIGURATION DU FIREWALL ---
  config.vm.define "firewall" do |fw|
    fw.vm.hostname = "firewall"
    # Interface 2 : DMZ (Réseau privé)
    fw.vm.network "private_network", ip: "192.168.100.1"
    # Interface 3 : LAN (Réseau privé)
    fw.vm.network "private_network", ip: "192.168.10.1"
    
    fw.vm.provider "vmware_desktop" do |v|
      v.gui = false # On reste en mode console
      v.vmx["memsize"] = "1024" # 1 Go de RAM
    end
  end

  # --- CONFIGURATION DU SERVEUR WEB ---
  config.vm.define "webserver" do |web|
    web.vm.hostname = "web-server"
    web.vm.network "private_network", ip: "192.168.100.10" # Dans la DMZ
  end

  # --- CONFIGURATION DE LA DB ---
  config.vm.define "dbserver" do |db|
    db.vm.hostname = "db-server"
    db.vm.network "private_network", ip: "192.168.10.10" # Dans le LAN
  end
end
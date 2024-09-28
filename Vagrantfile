MACHINES = {
  :frontend => {
        :vm_name => "frontend",
        :cpus => 1,
        :memory => 512,
        :ip => "192.168.56.101",
        :ip_public => "192.168.1.101",
        :ports => [
            {host: 8080, guest: 80},
            {host: 8443, guest: 443}
        ],
  },
  :backend_1 => {
        :vm_name => "backend-1",
        :cpus => 1,
        :memory => 768,
        :ip => "192.168.56.102",
  },
  :backend_2 => {
        :vm_name => "backend-2",
        :cpus => 1,
        :memory => 768,
        :ip => "192.168.56.103",
  },
  :db_master => {
        :vm_name => "db-master",
        :cpus => 1,
        :memory => 1024,
        :ip => "192.168.56.104",
  },
  :db_slave => {
        :vm_name => "db-slave",
        :cpus => 1,
        :memory => 1024,
        :ip => "192.168.56.105",
  },
  :monitoring => {
        :vm_name => "monitoring",
        :cpus => 2,
        :memory => 1024,
        :ip => "192.168.56.106",
        :ports => [
            {host: 3000, guest: 3000},
            {host: 9090, guest: 9090}
        ],
  },
  :log => {
        :vm_name => "log",
        :cpus => 6,
        :memory => 4608,
        :ip => "192.168.56.107",
        :ports => [
            {host: 9200, guest: 9200},
            {host: 5601, guest: 5601}
        ],
  }
}

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    config.vm.define boxname do |box|
      box.vm.box = "ubuntu/jammy64"
      box.vm.host_name = boxconfig[:vm_name]
      box.vm.network "private_network", ip: boxconfig[:ip]
      if boxconfig[:ip_public]
        box.vm.network "public_network", ip: boxconfig[:ip_public]
      end
      if boxconfig[:ports]
        boxconfig[:ports].each do |port|
          box.vm.network "forwarded_port", guest: port[:guest], host: port[:host], auto_correct: true
        end
      end
      box.vm.provider "virtualbox" do |vb|
        vb.memory = boxconfig[:memory]
        vb.cpus = boxconfig[:cpus]
        vb.name = boxconfig[:vm_name]
      end
      
      ssh_pub_key = File.readlines("../id_rsa.pub").first.strip
      box.vm.provision "shell", inline: <<-SHELL
       # mkdir ~root/.ssh
        echo #{ssh_pub_key} >> ~vagrant/.ssh/authorized_keys
        echo #{ssh_pub_key} >> ~root/.ssh/authorized_keys
        sudo sed -i 's/\#PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
        systemctl restart sshd
      SHELL
    end
  end
end

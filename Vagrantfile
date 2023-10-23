# -*- mode: ruby -*-
# vi: set ft=ruby :

GLOBAL_VARS ={vagrant: true}

MACHINES = {
  :htpc => {
    :box_name => "archlinux/archlinux",
    :net => [
    ],
    :vars => {}
  },
}
 

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    config.vm.define boxname do |box|
#        config.vm.box_check_update = false
        config.vm.box = boxconfig[:box_name]
        config.vm.provider :virtualbox do |vb|
          vb.gui = true
          vb.check_guest_additions = true
          vb.memory = 8192
          vb.cpus = 5
          vb.customize [
            "modifyvm", :id, "--uartmode1", "disconnected",
            "--paravirtprovider", "hyperv",
            "--graphicscontroller", "vmsvga",
            "--accelerate3d", "on",
            "--cpuexecutioncap", "70",
            "--vram", "256",
            "--ioapic", "on",
            "--audioout", "on",
            "--audioin", "on",
            "--audio", "default",
            "--audiocontroller", "hda"
            # "--clipboard-mode", "bidirectional"
          ]
        end
        box.vm.host_name = boxname.to_s
        box.vm.synced_folder "./packages/", "/mnt/"
        box.vm.provision "shell", privileged: true, inline: <<-SHELL
          #pacman -Syu --noconfirm
          #pacman -S python --noconfirm
          echo 'PermitRootLogin yes'  | sudo tee -a /etc/ssh/sshd_config
          echo -e "3241\n3241" | passwd root
          echo 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDm1yRtIE3esvnmlesO+q33vYYd0eyKBMh/Bx2PIAE1fWuxWcTdIn+9FPUTADlS4On6V9Dq0m4OGNSfoUbmvSy9obkfX4WIfuOJ9JY4T6CQ7xFy0XN65Ognqr8WRPMXE7aFMpLWkgQbiV1Pib29mUN0V0WBoJQJt2h2FgdZFcKpFYZTVWz6EWZIuUuSbBemlq/5ssWn75c83ZXH3ErgAz8hZznXNQsViwjd/cDv6UBpUjQlX4OD6QBVxnRZTKuXapmwcHGd9IkmhNLgug4dV9VUjMIk6ObVT9SLeRgKpBo9EMe7SJHL/9YFUr/GPPDKJIFZBh9GwIMOgkY/tLO+fsQH6GsluxFIh1CIrqSCP5BZSljusYeoeE0jukRk0HH+s7buMihzcgc+sZY43eWn4zyqWutompSxUKozzVhuW+wGFvfBWaX54QJFmjubI7CwuVJipeCgF29xo/2iwTxdOt3FoT/TxLX3TJF2c49cLSTF69CqzE2NIcrl9tph30/cgfs= michael@home-pc' | sudo tee /root/.ssh/authorized_keys
          chmod 600 /root/.ssh/authorized_keys
          pacman -U /mnt/python/*.tar.zst --noconfirm
          systemctl restart sshd
          SHELL
        box.vm.provision "ansible" do |ansible|
          ansible.compatibility_mode = "2.0"
          ansible.playbook = "playbook.yaml"
          ansible.extra_vars = GLOBAL_VARS.merge(boxconfig[:vars]).merge({host_name: boxname.to_s})
        end
    end
  end
end
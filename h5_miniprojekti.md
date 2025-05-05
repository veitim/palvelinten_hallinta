# h5 Miniprojekti

sudo wget https://archive.kali.org/archive-keyring.gpg -O /usr/share/keyrings/kali-archive-keyring.gpg


install_fuff:
  pkg.installed:
    - name: ffuf
  
install_zap:
  pkg.installed:
    - name: zaproxy
    
install_hashid_hashcat:
  pkg.installed:
    - name: hashid
    - name: hashcat
      
/home/vagrant/wlists:
  file.directory:
    - user: vagrant
    - group: vagrant                                                                                  
    - makedirs: True

getwlist:
  - file.managed:
    - name: /home/vagrant/wlists/rockyou.txt.tar.gz
    - source: https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz  
##


## Lähteet:

T. Karvinen 2025: Palvelinten Hallinta. Luettavissa: (https://terokarvinen.com/palvelinten-hallinta/) Luettu 6.5.2025

T. Karvinen 2025: Tunkeutumistestaus. Luettavissa: (https://terokarvinen.com/tunkeutumistestaus/) Luettu 6.5.2025

T. Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves (https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file) Luettu 6.5.2025

Kali inside Vagrant (Guest VM). Luettavissa: (https://www.kali.org/docs/virtualization/install-vagrant-guest-vm/) Luettu 6.5.2025

S. Gatlan 2025: Kali Linux warns of update failures after losing repo signing key. Luettavissa: (https://www.bleepingcomputer.com/news/linux/kali-linux-warns-of-update-failures-after-losing-repo-signing-key/) Luettu 6.5.2025

# h5 Miniprojekti

Init.sls:

    ffuf:
      pkg.installed
  
    nmap:
      pkg.installed
  
    hashid:
      pkg.installed
  
    hashcat:
      pkg.installed
  
    bash-completion:
      pkg.installed
  
    git:
      pkg.installed
  
    build-essential:
      pkg.installed
  
    libssl-dev:
      pkg.installed
  
    zlib1g:
      pkg.installed
  
    zlib1g-dev:
      pkg.installed
  
    libbz2-1.0:
      pkg.installed
  
    libbz2-dev:
      pkg.installed
  
    atool:
      pkg.installed
  
    zip:
      pkg.installed
  
    wget:
      pkg.installed
  
    create_directory:
      file.directory:
        - name: /home/vagrant/johntripper
        - user: vagrant
        - group: vagrant
        - makedirs: True
    
    john_the_ripper:
      git.latest:
        - name: https://github.com/openwall/john.git
        - target: /home/vagrant/johntripper
        - user: vagrant
        - rev: bleeding-jumbo
        - depth: 1  

## Lähteet:

T. Karvinen 2025: Palvelinten Hallinta. Luettavissa: (https://terokarvinen.com/palvelinten-hallinta/) Luettu 6.5.2025

T. Karvinen 2025: Tunkeutumistestaus. Luettavissa: (https://terokarvinen.com/tunkeutumistestaus/) Luettu 6.5.2025

T. Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves (https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file) Luettu 6.5.2025

Kali inside Vagrant (Guest VM). Luettavissa: (https://www.kali.org/docs/virtualization/install-vagrant-guest-vm/) Luettu 6.5.2025

S. Gatlan 2025: Kali Linux warns of update failures after losing repo signing key. Luettavissa: (https://www.bleepingcomputer.com/news/linux/kali-linux-warns-of-update-failures-after-losing-repo-signing-key/) Luettu 6.5.2025

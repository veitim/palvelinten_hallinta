# h4 Pkg_file_service

Tämä raportti on kirjoitettu 21.4.2025 klo. 15.30 -  välisenä aikana.

Raportissa on tehty Tero Karvisen Palvelinten Hallinta kurrsin tehtäviä, jotka löytyvät materiaaleineen sivustolta: (https://terokarvinen.com/palvelinten-hallinta/)

Käytetty laitteisto:

Isäntäkone:

Malli: Msi GE75 Raider 10sf
OS: Windows 10 Home 64-bit
RAM: 16 GB
CPU: Intel(R) Core(TM) i7-10750H CPU @ 2.60GHz (12 CPUs), ~2.6GHz
GPU: NVIDIA GeForce RTX 2070
BIOS: E17E9IMS, 10A

## x) Tiivistelmä

### Karvinen 2018: [Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)

* 
* 

## a) Asenna Apache, korvaa sen testisivu ja varmista, että demoni käynnistyy.

poistin apache2 käyttäen salttia komennolla: 

    sudo salt-call --local -l info state.single pkg.removed apache2



## b) SSHouto. Lisää uusi portti, jossa SSHd kuuntelee.

## c) v Asenna ja konfiguroi Apache ja Name Based Virtual Host

## d) v Caddy. Asenna Caddy tarjoilemaan weppisivua.

## e) v Nginx. Asenna Nginx (lausutaan engine-X) tarjoilemaan weppisivua. 
 
## f) v PostgreSQL. Asenna PostgreSQL-tietokannanhallintajärjestelmä.

## Lähteet: 

T. Karvinen 2025: Palvelinten Hallinta. Luettavissa: (https://terokarvinen.com/palvelinten-hallinta/) Luettu 21.4.2025

T. Karvinen 2018: Palvelinten Hallinta. Luettavissa: (https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh) Luettu 21.4.2025

Salt Project: Salt States. Luettavissa: (https://docs.saltproject.io/salt/user-guide/en/latest/topics/states.html) Luettu 21.4.2025

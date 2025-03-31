## h1 Viisikko
Tämä raportti on kirjoitettu 31.3.2025
Raportissa on tehty Tero Karvisen Palvelinten Hallinta kurrsin tehtäviä, jotka löytyvät sivustolta: (https://terokarvinen.com/palvelinten-hallinta/)

Käytetty laitteisto:
Isäntäkone:

* Malli: Msi GE75 Raider 10sf
* OS: Windows 10 Home 64-bit
* RAM: 16 GB
* CPU: Intel(R) Core(TM) i7-10750H CPU @ 2.60GHz (12 CPUs), ~2.6GHz
* GPU: NVIDIA GeForce RTX 2070
* BIOS: E17E9IMS, 10A

Virtuaalikone:
* OS: Debian/GNU Linux 12 (bookworm) x84_64
* RAM: 4 GB
* CPU: 2 processor
* GPU: 128 MB

### Tiivistelmä

### b) Salt-minion
Tehtävän aloitus kello 15.00

Avasin saltin asennus ohjeet: (https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html)

Asensin paketit komennoilla:

  "mkdir -p /etc/apt/keyrings" Teki hakemiston "keyrings" polkuun "/etc/apt/keyrings/"

  ![b](images/h1_b1.png)  
  
  "curl -fsSL https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public | sudo tee /etc/apt/keyrings/salt-archive-keyring.pgp" Jos oikein ymmärrän, niin tarkastelee linkkiä ja "tee" komennolla vie linkin datan keyrings hakemistoon tiedostoksi "salt-archieve-keyring.pgp"

  ![b](images/h1_b2.png)

  "curl -fsSL https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources | sudo tee /etc/apt/sources.list.d/salt.sources" Sama toistuu, eli linkin takana olevat tiedot viedään hakemistoon tiedostoksi "salt.sources"

  ![b](images/h1_b6.png)
   
Seuraavaksi yritin asentaa salt-minionin komennolla "sudo apt-get install -y salt-minion"

![b](images/h1_b4.png)

Ei onnistunut, pakettien kanssa jotain häiriötä. Olin unohtanut vaiheen 2 asennus ohjeesta. Eli pakettien päivityksen. Komennolla "sudo apt update" paketit päivitettiin ja tämän jälkeen kokeilin uudestaan salt-minionin asentamista ja se toimi. Tarkistus komennolla "sudo salt-call --version"

![b](images/h1_b5.png)

Valmis 16.00

### c) Viisi Tärkeintä

### d) Idempotentti

### Lähteet:

Karvinen, Tero 2025: Palvelinten Hallinta: (https://terokarvinen.com/palvelinten-hallinta/) Luettu 31.3.2025

Karvinen, Tero 2018: Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux: (https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/) Luettu 31.3.2025

Karvinen, Tero 2006: Raportin Kirjoittaminen: (https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/) Luettu 31.3.2025

Karvinen, Tero 2023: Run Salt Command Locally: (https://terokarvinen.com/2021/salt-run-command-locally/) Luettu 31.3.2025

Salt Project, Linux (DEB): (https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html) Luettu 31.3.2025

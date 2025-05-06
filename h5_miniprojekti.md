# h5 Miniprojekti

Elikkä miniprojektina on pentesting labra debianille. Tarkoituksena on vagrantilla tehdä debian kone, jolla voi harjoutella hyökkäämistä ja maalikone mihin voi hyökätä.

Aloitin tekemällä moduulin, mikä asentaa hyökkäämiseen soveltuvia ohjelmia. Tein tälle init.sls oman [repon](https://github.com/veitim/miniprojekti/blob/main/init.sls), jonka haen vagranfilellä konetta alustaessa. 

![a](images/h5_1.png)

![a](images/h5_1.png)

![a](images/h5_1.png)

Moduuli "attax" suoritetaan komennolla:

    sudo salt-call --local state.apply attax

Tämä täytyy tehdä kolme kertaa, jotta saavutetaan idempotentti tila.

![a](images/h5_4.png)



![a](images/h5_5.png)

* ffuf - fuzzaus työkalu (dokumentaatio: https://github.com/ffuf/ffuf)
* nmap - työkalu porttiskannausta varten (dokumentaatio: https://nmap.org/docs.html)
* hashid - Kertoo minkä tyyppinen hashi on kyseessä
* hashcat - salasanan murtamista (dokumentaatio: https://hashcat.net/wiki/doku.php?id=hashcat)
* bash-completion - john the ripperin vaatimus. "make" komento käyttää tätä
* git - john the ripperin asentamista varten.
* build-essential - john the ripperin vaatimus
* libssl-dev - john the ripperin vaatimus
* zlib1g - john the ripperin vaatimus
* zlib1g-dev - john the ripperin vaatimus
* libbz2-1.0 - john the ripperin vaatimus
* libbz2-dev - john the ripperin vaatimus
* atool - john the ripperin vaatimus
* zip - john the ripperin vaatimus
* wget - john the ripperin vaatimus
* Loput on sitten john the ripperin asentelua. Alkuun tehdään hakemisto john the ripperille. Tämän jälkeen asennetaan tämä hakemalla se tekijän github reposta. (johnin dokumentaatio: https://github.com/openwall/john)

Pieni demo johh the ripperistä:

Navigoidaan seuraavaan hakemistoon ja suoritetaan ./configure

![a](images/h5_7.png)

Tämän jälkeen suoritetaan seuraavassa kuvassa näkyvä "make" komento

![a](images/h5_8.png)

    make -s clean && make -sj2" 

Työkaluvalmiina käytettäväksi

![a](images/h5_9.png)

Jokunen työkalu millä tehdä ikävyyksiä.

![a](images/h5_10.png)

Seuraavaksi tehdään tiedosto, joka zipataan ja salasanalla suojataan.

![a](images/h5_6.png)



## Lähteet:

T. Karvinen 2025: Palvelinten Hallinta. Luettavissa: (https://terokarvinen.com/palvelinten-hallinta/) Luettu 6.5.2025

T. Karvinen 2025: Tunkeutumistestaus. Luettavissa: (https://terokarvinen.com/tunkeutumistestaus/) Luettu 6.5.2025

T. Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves (https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file) Luettu 6.5.2025

T. Karvinen 2023: Crack File Password With John. Luettavissa: (https://terokarvinen.com/2023/crack-file-password-with-john/) Luettu 6.5.2025

T. Karvinen 2022: Cracking Passwords with Hashcat. Luettavissa: (https://terokarvinen.com/2022/cracking-passwords-with-hashcat/) Luettu 6.5.2025

Hashi Corp: rapid7/metasploitable3-win2k8. Luettavissa: (https://portal.cloud.hashicorp.com/vagrant/discover/rapid7/metasploitable3-win2k8) Luettu 6.5.2025

Salt Project: How Do I Use Salt States?: Luettavissa: (https://docs.saltproject.io/en/latest/topics/tutorials/starting_states.html) Luettu 6.5.2025

I. Das 2023: Youtube video: Metasploitable 3 Win2k8 Installation Guide with Windows PowerShell, Vagrantfile and Vagrant Cloud: Katsottavissa: (https://www.youtube.com/watch?v=5MaIR-2ND7o) Katsottu 6.5.2025

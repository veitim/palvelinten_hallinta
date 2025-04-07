# h2 Soitto Kotiin

Tämä raportti on kirjoitettu 7.4.2025 klo. 14.00 -  välisenä aikana.

Raportissa on tehty Tero Karvisen Palvelinten Hallinta kurrsin tehtäviä, jotka löytyvät materiaaleineen sivustolta: (https://terokarvinen.com/palvelinten-hallinta/)

Käytetty laitteisto:

Isäntäkone:

* Malli: Msi GE75 Raider 10sf
* OS: Windows 10 Home 64-bit
* RAM: 16 GB
* CPU: Intel(R) Core(TM) i7-10750H CPU @ 2.60GHz (12 CPUs), ~2.6GHz
* GPU: NVIDIA GeForce RTX 2070
* BIOS: E17E9IMS, 10A

## x) tiiviste

###

###

###

## a) Hello vagrant!

Latasin vagrantin sivustolta: (https://developer.hashicorp.com/vagrant/install)

Valitsin seuraavan version, koska käytän windowsia.

[a](images/h2_a1.png)

Asensin ohjelman ajamalla tämän tuplaklikkaamalla installer-kuvaketta. Asennuksen jälkeen käynnistin koneen uudeestaan.

Windowsin komentotulkissa komennolla "vagrant version" pystyi tarkistamaan, että onko vagrant asennettuna. (Vagrantin dokumentaatiot löytyvät osoitteesta: https://developer.hashicorp.com/vagrant/docs)

[a](images/h2_a2.png)

Näyttäisi olevan.

## b) Vagrantilla uusi linux virtuaalikone

Lueskelin Antti Salmisen raporttia: (https://oispadotka.wordpress.com/2020/05/12/h6/) ja lähdin kokeilemaan.

Käytin komentoa "vagrant box add hashicorp/bionic64", mikä asensi kehitysympäristön. Jos oikein olen ymmärtänyt, niin tämä asensi asetukset bionic64 käyttöjärjestelmää varten. Tämä on Stephen Jenningsin mukaan Ubuntu 18.04 versio. Eli en uskoakseni olisi tarvinnut tätä asennusta, koska aion käyttää debiania. Tämän lisäksi asensin boxin C-asemalle, minne tätä en halua.

[b](images/h2_b1.png)

Tein tässä vaiheessa uuden hakemiston D-asemalle ja navigoin komentutulkissa tänne. Tänne aion siis asentaa vagrantilla virtuaalikoneita. Kokeilin Karvisen sivulta löytyvää "init debian/bookworm64" komentoa, minkä pitäisi virtuaalikone alustaa.

[b](images/h2_b2.png)

Tämä onnistui eli nyt on vagrantfile ja pitäisi pystyä virtuaalikone käynnistämään komennolla "vagrant up".

[b](images/h2_b3.png)

Boxia debian/bookworm64 ei löydy, mutta vagrant automaattisesti tämän boxin haki ja asensi, mikä teki aikaisemmasta boxin lisäämisestä todellakin turhan.

[b](images/h2_b4.png)

Virtuaalikone asennettu ja näyttää pyörivän.

## c) Kaksin kaunihimpi

Poistin aikaisemmin tekemäni virtuaalikoneen komennolla: "vagrant destroy".  Komento ei kuitenkaan vagranfileä poistanu, joten tätä ei tarvinnut erikseen luoda uudestaan. Seuraavaksi pähkäilin, että miten saan vagrantfileä konfiguroimalla tehtyä 2 virtuaalikonetta kerralla.

Karvisen materiaaleista (osoitteesta: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/) löytyikin vagrantfilen pohja millä saa kaksi virtuaalikonetta luotua. 

Jos osaan vagranfileä oikein tulkita, niin tämä tekee koneet t001 ja t002. Asettaa nämä verkkoon "192.168.88.101". Sekä ajaa scriptin, mikä suorittaa komennot:
* "set -o verbose" - Windows server docsien mukaan komento tekee seuraavan: Turns on verbose output logging during the shadow copy creation process. If verbose mode is on, set provides details of writer inclusion or exclusion and details of metadata compression and extraction. (https://github.com/MicrosoftDocs/windowsserverdocs/blob/main/WindowsServerDocs/administration/windows-commands/set-verbose.md)
* "apt-get update" - hakee paketeille päivitykset
* "apt-get -y install tree" - asentaa tree paketin
* 'echo "Done - set up test environment - https://terokarvinen.com/search/?q=vagrant"' - tulostaa viestin

Oletan, että scriptit ajetaan koneiden sisällä.

Muokkasin vagranfilestä aluksi riviä 'config.vm.box = "debian/bullseye64"' seuraavasti  'config.vm.box = "debian/bookworm64"' Koska bookworm on tutumpi. Eli virtuaalikoneet asentuvat debian bookworm ympäristöön bullseyen sijaan.

[c](images/h2_c1.png)

Sitten kokeilin "vagrant up" komentoa.

Sehän toimi ja koneet t001 ja t002 tehtiin debian/bookworm64 alustaa käyttäen. Paketit päivitettiin ja tree asennettiin sekä echolla myös viesti tulostettiin. Scriptiin voisi ehkä lisätä rivit "sudo apt-get -y install ufw" ja "sudo ufw enable" millä palomuuri asentuisi ja tulisi käyttöön koneille. Ja juuri tässä järjestyksessä, eli ensiksi asennetaan sitten otetaan käyttöön. 

Komennolla "vagrant ssh t001" kirjauidin t001 koneelle ja komennolla "ip addr" sain selville, että ip-osoite on yllättäen "192.168.88.101". "Exit komennolla kirjauduin ulos. Tarkistin myös t002 koneen ip:n (192.168.88.102) ja sitten pingasin t002 koneelta t001 koneen osoitetta komennolla "$ ping 192.168.88.101"

[c](images/h2_c2.png)

Koneet keskustelevat keskenään.

## d) herra-orja

Aloitin tuhoamalla virtaalikoneet käyttäen komentoa "vagrant destroy".

Seuraavaksi muokkasin vagrantfileä seuraavasti

[d](images/h2_d1.png)

Eli lisäsin palomuurin asennuksen ja käyttöön oton ja nimesin ensimmäisen koneen masteriksi sekä toisen koneen s001:ksi.

Sitten taast ajamaan komentoa "vagrant up". Epäonnistuin, sillä unohdin tallentaa vagrantfileen tehdyt muutokset. Vagrantti lähti siis ajamaan vagrantfileä aiemmilla konfiguraatioilla, eli "t001 ja t002 jne.."

Uusi yritys tallennuksen jälkeen. Muuten näyttäisi onnistuneen, mutta palomuurin päälle laittaminen ei onnistuinut.

[d](images/h2_d2.png)

Seuraavaksi kirjauduin master koneelle ja pingasin s001 konetta sekä laitoin palomuurin päälle. Sitten avastin portit 4505/tcp ja 4506/tcp komennolla "sudo ufw allow 'portti'" Tämän jälkeen kävin laittamassa s001 koneelta palomuurin päälle. Sitten buuttasin koneet "vagrant halt" sammuttaa ja "vagrant up" käynnistää.

Palomuuri näytttäisi estävän vagrantilta pääsyn koneelle. Eli alusta. Tuhosin koneet. Muokkasin vagrantfileä siten, ettei koneet yritä käynnistää palomuuuria. Asesnsin koneet.

Muistaakseni ssh käyttää porttia 22, joten avasin kyseisen portin sekä portit 4505 ja 4506 master koneelta. Käynnistin palomuurin ja buuttasin koneet.

Näyttäisi toimivan, joten käynnistin koneelta s001 palomuurin ja avasin reiän 22, jotta ssh pääsee palomuurin ohi. Uudestaan buuttaus.

Kirjauduin master koneelle ja pingasin s001 konetta.

Näyttäisi toimivan, joten seuraavaksi asensin salt masterin. Tässä vaiheessa heräsi ajtus, että nämä salt pakettien asennukset voisi kyllä viedä vagrantfileen. Päätin kokeilla mitä käy, jos vain asentaa salt-maseterin master koneelle ja salt-minionin s001 koneelle. Uskoisin, että homma ei toimi.

Pitkälle ei päästy, koska salt paketit puuttuvat. Sammutin koneet. Ja kävin päivittämässä vagrantfileä.

Lisäsin tiedostoon saltpakettien asennus komennot, näin muodostaen luottamussuhteen. Seuraavaksi kokeilin komentoa "vagrant reload" komentoa minkä pitäisi uudeelleen käynnistää koneet samalla lataamalla uudet konfiguraatiot vagrantfilestä. Paketit eivät näin asentuneet. Kokeilen vielä "vagrant reload --provision" komentoa.

Harmi, curl komentoa ei löydy joten paketit eivät kansioihin tulleet. En jaksa tässä vaiheessa selvittämään, että millä komennolla rubyllä tämän voisi tehdä, joten asennan paketit koneille manuaalisesti. Kävin kanssa poistamassa vagranfilestä komennot millä lisätään paketit.

[d](images/h2_d3.png)

[d](images/h2_d4.png)

## e) Kokeile vähintään kahta tilaa verkossa

## Lähteet:

T. Karvinen 2025: Palvelinten Hallinta: Luettavissa: (https://terokarvinen.com/palvelinten-hallinta/) Luettu 7.4.2025

T. Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. Luettavissa: (https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/) Luettu 7.4.2025

T. Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: (https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/) Luettu 7.4.2025

T. Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves. Luettavissa: (https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file) Luettu 7.4.2025

A. Salminen: h6. Luettavissa: (https://oispadotka.wordpress.com/2020/05/12/h6/) Luettu 7.4.2025

HashiCorp: Installa Vagrant. Luettavissa: (https://developer.hashicorp.com/vagrant/install) Luettu 7.4.2025

HashiCorp: Vagrant Documentation. Luettavissa: (https://developer.hashicorp.com/vagrant/docs) Luettu 7.4.2025

Stack Overflow: Viestiketju, What is the difference between hashicorp/precise64 and hashicorp/bionic64?. Luettavissa: (https://stackoverflow.com/questions/70702895/what-is-the-difference-between-hashicorp-precise64-and-hashicorp-bionic64#70703021) Luettu 7.4.2025

wpscholar: Vagrant Cheat Sheet. Luettavissa: (https://gist.github.com/wpscholar/a49594e2e2b918f4d0c4) Luettu 7.4.2025

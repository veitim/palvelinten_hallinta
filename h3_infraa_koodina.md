# h3 Infraa Koodina

Tämä raportti on kirjoitettu 14.4.2025 klo. 14.30 -  välisenä aikana.

Raportissa on tehty Tero Karvisen Palvelinten Hallinta kurrsin tehtäviä, jotka löytyvät materiaaleineen sivustolta: (https://terokarvinen.com/palvelinten-hallinta/)

Käytetty laitteisto:

Isäntäkone:

    Malli: Msi GE75 Raider 10sf
    OS: Windows 10 Home 64-bit
    RAM: 16 GB
    CPU: Intel(R) Core(TM) i7-10750H CPU @ 2.60GHz (12 CPUs), ~2.6GHz
    GPU: NVIDIA GeForce RTX 2070
    BIOS: E17E9IMS, 10A


## x) Tiiviste

### Hello Salt Infra-as-Code

* Saltilla voit hallita tuhansia koneita.

Saltin-asennus

* $ sudo apt-get update
* $ sudo apt-get -y install salt-minion/master

Moduuli

* $ sudo mkdir -p /srv/salt/hello/ - "/hello/" on moduuli mitä käytetään.
* $ cd /srv/salt/hello/ - "/srv/salt/" jaetaan orjille.
* $ sudoedit init.sls - Täytyy olla moduulissa mitä halutaan käyttää (tässä tapauksessa se on "/hello/").
* $ sudo salt-call --local state.apply hello - ajaa moduulin "hello"

Micro editor

* $ sudo apt-get -y install micro - asentaa micron
* $ export EDITOR=micro - asettaa micron oletus editoriksi

### Salt Overview

Rules of YAML

* YAML -> Pythoniksi salttia varten
* Data on rakenteellista "avain: arvo" -> "hedelmä: omena"
* CASE-SENSITVE (isolla ja pienellä kirjaimella merkitystä)
* Sisennykset tapahtuvat välilyönnillä (ei saa käyttää TAB-painiketta)
* Kommentit alkavat risuaidalla "#"

YAML simple structure

Scalars, arvo voi olla numero, teksti tai boolean (true/false)

* avain: arvo" -> "hedelmä: omena"

Lists, arvot menevät omille riveille kahden välilyönnin ja väliviivan kanssa. 

    lista_avain:
      - arvo1
      - arvo2

Dictionaries

    kirja_avain:
      avain: arvo   
      lista_avain:
        - arvo1
        - arvo2

Lists and dictionaries - YAML block structures

* YAML on lohkoissa
* Arvot pitää sisentää yhdellä tai useammalla välilyönnillä (2 standardi)
* Listoissa pitää käyttää väliviivaa ja välilyöntiä

## a) Hei infrakoodi

Navigoin komentotulkissa hakemistoon missä vagranfile sijaitsee ja käynnistin virtuaalikoneet komennolla: "vagrant up".

Kirjaudin master koneelle komennolla "vagrant ssh master" ja tein komennolla "sudo mkdir -p /srv/salt/hello/" kansion "hello" hakemistoon "/srv/salt/". Kansiota "hello" käytetään tässä tehtävässä moduulina.

![a](images/h3_a1.png)

Tämän jälkeen navigoin juuri tekemääni hakemistoon "cd /srv/salt/hello/". Asetin micron oletuseditoriksi ja tein init.sls tiedoston komennolla "sudoedit init.sls" Ja lisäsin tänne seuraavat rivit:

    /tmp/hellotimo:
      file.managed
 
Seuraavaksi ajoin tekemääni moduulia lokaalisti komennolla "sudo salt-call --local state.apply hello".

![a](images/h3_a2.png)

## b) Aja esimerkki sls-tiedostosi verkon yli

## c) Sls-tiedosto 2 tilafunktiolla

## Lähteet:

T. Karvinen 2014: Hello Salt Infra-as-Code. Luettavissa: (https://terokarvinen.com/2024/hello-salt-infra-as-code/) Luettu 14.4.2025

Salt Project: Salt overview. Luettavissa: (https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml) Luettu 14.4.2025



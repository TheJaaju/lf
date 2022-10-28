# Ohjeet CS:GO serverin asentamiseen - Jami Juva 2022

``OS: Ubuntu-Server 22.04 LTS x86_64``

## Tarvittavat asiat:
    - steamcmd
    - CS:GO Dedicated server (CSGO-DS)

## 1. Steamcmd

### Luodaan steamille oma käyttäjä sudo:na ja annetaan sille salasana
```
sudo useradd -m steamcmd
sudo passwd steam

(testipalvelimen salasanaksi esim. kanakeitto)
```

### steamcmd:n lataus

#### 64 bittisellä koneella:
```
sudo add-apt-repository multiverse
sudo apt install software-properties-common
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install lib32gcc-s1 steamcmd
```
#### Ladataan steamcmd
 ``sudo apt install steamcmd``

lisenssikysymyksissä vaan ``OK`` ja ``I AGREE``

#### Linkataan steamcmd:n executable
 ``sudo ln -s /usr/games/steamcmd /home/steam/steamcmd``


### Rakennetaan pelipalvelimen tiedostopolku ``/opt/`` directoryyn
    sudo mkdir /opt/csgo-ds

### Vaihdetaan steam käyttäjään ja käynnistetään steamcmd
    sudo -u steam -s
    steamcmd
### Mahdollisesti vastaantuleva ongelma
    The command could not be located because '/usr/games' is not included in the PATH

    environment variable. steamcmd: command not found
fix:

``export PATH="/usr/games:$PATH"``

## 2. CS:GO DS
### Palvelimen Lataaminen
```bash
# steam käyttäjänä:
#2.1 Käynnistetään steamcmd:
    steamcmd

#2.2 asetetaan asennuskansio /opt/csgo-ds
    force_install_dir /opt/csgo-ds

#2.3 Kirjaudutaan sisään anonyymillä käyttäjällä
    login anonymous

#2.4 Asennetaan pelipalvelin ja tarkistetaan tiedostot
    app_update 740 validate

# Palvelimen päivitys:
    app_update 740

# steamcmd saattaa kaatuilla latauksen aikana, tällöin aloitetaan vain kohdasta 2.1
```
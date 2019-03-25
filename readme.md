# M300 - LB2 Dokumentation Silvan Walz*

Die nachstehende Dokumentation zeigt alle Schritte auf, die ich während der LB2 gemacht habe.

## Inhaltsverzeichnis
- [M300 - LB2 Dokumentation Silvan Walz*](#m300---lb2-dokumentation-silvan-walz)
  - [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [K1](#k1)
  - [Vagrant](#vagrant)
  - [Visual Studio Code](#visual-studio-code)
  - [Git-Client](#git-client)
  - [SSH-Key](#ssh-key)
- [K2](#k2)
  - [GitHub Account](#github-account)
- [K4](#k4)
___

K1
======

> [⇧ **Nach oben**](#inhaltsverzeichnis)
 
  ## VirtualBox

1. Als erstes habe ich auf [dieser Webseite](https://www.virtualbox.org) VirtualBox heruntergeladen und danach GUI-basiert installiert.
2. Danach habe ich den Ubuntu Desktop 16.04.05 auf [dieser Webseite](https://www.ubuntu.com/#download) heruntergeladen. 

**Nachdem ich das ISO heruntergeladen habe, habe ich die VM erstellt:**
1. VirtualBox starten
2. Mit einem klick auf `Neu` eine neue VM erstellen.
3. Als nächstes muss man folgende Attribute angeben:
   *  Name:           `M300_Ubuntu_XX.04_Desktop`
   *  Typ:            `Linux`
   *  Version:        `Ubuntu (64-bit)`
   *  Speichergrösse: `2048 MB`
   *  Platte:         `[X] Festplatte erzeugen`
4. Nun auf `Erzeugen` klicken
5. Im nächsten Fenster, folgende Informationen eintragen:
   *  Dateipfad:                       standard
   *  Dateigrösse:                     `10.00 GB`
   *  Dateityp der Festplatte:         `VMDK (Virtual Maschine Disk)`
   *  Storage on physical hard disk:   `dynamisch alloziert`
6. Nun erneut auf `Erzeugen` klicken, dann im Hauptmenü die VM anwählen (blau markiert) und den Punkt `Ändern` aufrufen
7. Im Abschnitt `Massenspeicher` den SATA-Controller anwählen und auf das CD+Symbol klicken
8. Unter `Medium auswählen` das zuvor heruntergeladene Systemabbild (ISO-Datei) anwählen
9. Alle Änderungen speichern und die VM starten
10. Nun den Installationsanweisungen der OS-Installation folgen. 

Nun ist die VM erstellt.

**Danach habe ich in der Bash folgende Befehle ausgeführt.**

1. Paketliste neu einlesen und Pakete aktualisieren:
   ```Shell 
   $  sudo apt-get update   #Paketlisten des Paketmanagement-Systems "APT" neu einlesen
   
   $  sudo apt-get update   #Installierte Pakete wenn möglich auf verbesserte Versionen aktualisieren

   $  sudo reboot           #System-Neustart durchführen
   ```
2. Software Controlcenter "Synaptic" installieren:
   ```Shell 
   $  sudo apt-get install synaptic
   ```
3. Nach erfolgreicher Installation in der Suche nach "Synaptic Package Manager" suchen und diesen starten
4. Innerhalb des Managers nach "apache" (Webserver-Programm) suchen und dieses (inkl. aller Abhängigkeiten) installieren
5. System-Neustart durchführen:
   ```Shell 
   $  sudo reboot
   ```
6. Danach habe geprüft, ob der Standard-Content des Webservers unter "http://127.0.0.01:80" erreichbar ist


## Vagrant
> [⇧ **Nach oben**](#inhaltsverzeichnis)

Zuerst habe ich Vagrant auf [dieser Webseite](https://www.vagrantup.com/ "vagrantup.com")   heruntergeladen und GUI-Basiert installiert.

**Danach habe ich mit Vagrant eine VM erstellt.**
1. Terminal öffnen
2. Einen neuen Ordner für die VM anlegen:
    ```Shell
      $ cd C:\Users\silva
      $ mkdir MeineVagrantVM
      $ cd MeineVagrantVM
    ``` 
3. Vagrantfile erzeugen, VM erstellen und starten:
    ```Shell
      $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Netzwerkshare hinzufügen
      $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
      $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
    ``` 
4. Die VM ist nun bereit und kann mit SSH-Zugriff bedient werden:
    ```Shell
      $ cd C:\Users\silva\MeineVagrantVM      #Zum Verzeichnis der VM wechseln
      $ vagrant ssh                       #SSH-Verbindung zur VM aufbauen
    ``` 

**Nachfolgend habe ich eine VM mit Apache Webserver von einem bereits abgeänderten File erstellt:**

1. Terminal öffnen
2. In das M300-Verzeichnis wechseln:
    ```Shell
      $ cd C:\Users\silva\M300\vagrant\web
    ``` 
3. VM erstellen und starten:
    ```Shell
      $ vagrant up
    ``` 
4. Danach habe ich im Webbrowser geprüft, ob der Standard-Content des Webservers unter "http://127.0.0.01:8080" (localhost) erreichbar ist
5. Später habe ich im Ordner `\web` die Hauptseite `index.html` editiert und das Resultat überprüft.
6. Abschliessend habe ich die VM wieder gelöscht:
    ```Shell
      $ vagrant destroy -f
    ```

## Visual Studio Code
> [⇧ **Nach oben**](#inhaltsverzeichnis)

**In diesem Abschnit habe ich Visual Studio Code heruntergeladen, installiert und angewendet.**

1. Ich habe Visual Studio Code auf [dieser](https://code.visualstudio.com/"visualstudio.com") Seite heruntergelden und GUI-basiert installiert.
2. Danach habe ich dem Editor drei wichtige Extensions hinzugefügt:

* Markdown All in One (von Yu Zhang)
* Vagrant Extension (von Marco Stanzi)
* vscode-pdf Extension (von tomiko1207)

Dazu habe ich folgende Anweisungen befolgt: 

  1. Visual Studio Code öffnen
  2. Die Tastenkombination `CTRL` + `SHIFT` + `X` drücken und in der Suchleiste die erwähnten Extensions suchen
  3. Auf `Install` klicken und anschliessend auf `Reload`, um die Extension in den Arbeitsbereich zu laden.

**Um die Dokumentation lokal mit Visual Studio Code zu bearbeiten, arbeite ich folgendermassen:**

  1. Änderungen am Readme-File von meinem Repositorys vornehmen
  2. Datei speichern und in der linken Leiste das Symbol mit einer "1" aufrufen
  3. Unter dem Abschnitt **Changes** die betroffenen Files bezüglich ihres Changes "stagen"
  4. Nachricht hinterlegen und Haken setzen
  5. Bei den 3 Punkten (...) auf **Push** klicken
  6. Warten, bis Dateien vollständig gepusht wurden

## Git-Client
> [⇧ **Nach oben**](#inhaltsverzeichnis)

Damit ich die Arbeiten lokal auf dem eigenen PC machen konnte, musste ich der sogenannte "Git Client", auf Windows "Git/Bash" installieren. 

**Client installieren**
Ich habe Client-Installation auf [dieser](https://git-scm.com/downloads) Seite heruntergeladen und GUI-basiert installiert.

**Danach habe ich den Client konfiguriert:**
1. Terminal öffnen
2. Git konfigurieren mit Informationen des GitHub-Accounts:
    ```Shell
      $ git config --global user.name "<username>"
      $ git config --global user.email "<e-mail>"
    ``` 

**Damit ich das readme-File lokal bearbeiten kann, habe ich das Repository heruntergeladen und aktualisiert.**

1. Terminal öffnen
2. Ordner für Repository erstellen:
    ```Shell
      $ cd C:\Users\silva\Desktop
      $ mkdir githublb2
    ``` 
3. Repository mit SSH klonen:
    ```Shell
      $ git clone git@github.com:silvanwalz/lb2.git

      Cloning into 'lb2'...
    ``` 
4. Repository aktualisieren und Status anzeigen:
    ```Shell
      $ git pull

      Already up to date.
    ```

## SSH-Key 
> [⇧ **Nach oben**](#inhaltsverzeichnis)

**Zuerst musste ich Lokal einen SSH-Key erstellen:**

1.  Folgenden Befehl mit der Account-E-Mail von GitHub in Bash einfügen:
    ```Shell
      $  ssh-keygen -t rsa -b 4096 -C "silvan.walz@hotmail.ch"
    ```
2. Neuer SSH-Key wird erstellt:
    ```Shell
      Generating public/private rsa key pair.
    ```
3. Bei der Abfrage, unter welchem Namen der Schlüssel gespeichert werden soll, die Enter-Taste drücken (für Standard):
    ```Shell
      Enter a file in which to save the key (~/.ssh/id_rsa): [Press enter]
    ```
4. Nun habe ich ein Passwort für den Key festgelegt:
    ```Shell
      Enter passphrase (empty for no passphrase): [Passwort]
      Enter same passphrase again: [Passwort wiederholen]
    ```
**Danach kann ich den SSH-Key dem Client hinzufügen:**
1. Auf www.github.com im Benutzerkonto **Settings** aufrufen
2.  Unter den Menübereichen auf der linken Seite zum Abschnitt **SSH und GPG keys** wechseln
3.  Auf **New SSH key** klicken
4.  Im Formular unter **Title** die Bezeichnung MB SSH-Key vergeben
5.  Den Key von der Datei **C:\Users\silva\.ssh\id_rsa.pub** einfügen und auf **Add SSH key** klicken

___
K2
======
## GitHub Account
> [⇧ **Nach oben**](#inhaltsverzeichnis)

**Ich habe folgendermassen einen Github Account erstellt:**
1. Auf [GitHub.com](https://github.com) gehen
2. Auf **Sign up** klicken
3. Username, E-mail und Passwort eingeben sowie Aufgabe zum verifizieren lösen
4. Auf **Create an Account** klicken


K4
======

> [⇧ **Nach oben**](#inhaltsverzeichnis)
 
  ## Firewall
  
1. Vagrantfile öffnen
2. Folgende Zeilen einfügen:
    ```Shell
      sudo apt-get install ufw
      sudo ufw allow 80/tcp
      sudo ufw allow 22/tcp
      sudo ufw allow out 22/tcp 
      sudo ufw "enable"
    ``` 

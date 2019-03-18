# M300 - LB2 Dokumentation Silvan Walz

Die nachstehende Dokumentation zeigt alle Schritte auf, die ich während der LB2 gemacht habe.

### Inhaltsverzeichnis

* [K1](#K1)
  * [VirtualBox](#VirtualBox)
* 02 - [Vagrant](#02---vagrant)
* 03 - [Visual Studio Code](#03---visual-studio-code)
___

K1
======

> [⇧ **Nach oben**](#inhaltsverzeichnis)

## VirtualBox
Als erstes habe ich VirtualBox installiert. 

### Software herunterladen & installieren
***
1. Ich habe auf [dieser](https://www.virtualbox.org) Seite VirtualBox heruntergeladen.
2. Die Installation erfolgt danach GUI-basiert.

### ISO-Datei herunterladen
***
Danach habe ich den Ubuntu Desktop 16.04.05 auf [dieser](https://www.ubuntu.com/#download) Seite heruntergeladen. 

### VM erstellen
***
Nachdem ich das ISO heruntergeladen habe, bin ich folgendermassen fortgefahren:

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

### VM einrichten
***
Danach habe ich in der Bash folgende Befehle ausgeführt.

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

In diesem Abschnit habe ich Vagrant eingerichtet.

### Software herunterladen & installieren
***
Ich habe Vagrant auf [dieser](https://www.vagrantup.com/ "vagrantup.com")  Seite heruntergeladen und GUI-Basiert installiert.


### Virtuelle Maschine erstellen
***
Danach habe ich mit Vagrant eine VM erstellt.

1. Terminal öffnen
2. In Verzeichnis einen neuen Ordner für die VM anlegen:
    ```Shell
      $ cd C:\Users\silva
      $ mkdir MeineVagrantVM
      $ cd MeineVagrantVM
    ``` 
3. Vagrantfile erzeugen, VM erstellen und entsprechend starten:
    ```Shell
      $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Netzwerkshare hinzufügen
      $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
      $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
    ``` 
4. Die VM ist nun in Betrieb (erscheint auch in der Übersicht innerhalb von VirtualBox) und kann via SSH-Zugriff bedient werden:
    ```Shell
      $ cd C:\Users\silva\MeineVagrantVM      #Zum Verzeichnis der VM wechseln
      $ vagrant ssh                       #SSH-Verbindung zur VM aufbauen
    ``` 

### Virtuelle Maschine erstellen (mit Vagrant-Box auf Netzwerkshare)
***
1. Terminal öffnen
2. Einen neuen Ordner für die VM anlegen:
    ```Shell
      $ cd Wohin\auch\immer
      $ mkdir MeineVagrantVM
      $ cd MeineVagrantVM
    ``` 
3. Vagrantfile erzeugen, VM erstellen und starten:
    ```Shell
      $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Netzwerkshare hinzufügen, falls nicht vorhanden
      $ vagrant init ubuntu/xenial64                                                      #Vagrantfile erzeugen
      $ vagrant up --provider virtualbox                                                  #Virtuelle Maschine erstellen & starten
    ``` 
4. Die VM ist nun in Betrieb (erscheint auch in der Übersicht innerhalb von VirtualBox) und kann via SSH-Zugriff bedient werden:
    ```Shell
      $ cd Pfad\zu\meiner\Vagrant-VM
      #Zum Verzeichnis der VM wechseln
      $ vagrant ssh             
      # SSH-Verbindung zur VM          
    ``` 

### Apache Webserver automatisiert aufsetzen
***
Nachfolgend habe ich die VM mit einem bereits abgeänderten File bzw. VM aus dem M300-Repository erstellt:

1. Terminal öffnen
2. In das M300-Verzeichnis (\M300\vagrant\web) wechseln:
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

In diesem Abschnit habe ich Visual Studio Code heruntergeladen und angewendet.

### Software herunterladen & installieren
***
1. Ich habe Visual Studio Code auf [dieser](https://code.visualstudio.com/"visualstudio.com") Seite heruntergelden und GUI-basiert installiert.


### Extensions installieren
***

Danach habe ich dem Editor drei wichtige Extensions hinzugefügt:

* Markdown All in One (von Yu Zhang)
* Vagrant Extension (von Marco Stanzi)
* vscode-pdf Extension (von tomiko1207)

Dazu habe ich folgende Anweisungen befolgt: 

1. Visual Studio Code öffnen
2. Die Tastenkombination `CTRL` + `SHIFT` + `X` drücken und in der Suchleiste die erwähnten Extensions suchen
3. Auf `Install` klicken und anschliessend auf `Reload`, um die Extension in den Arbeitsbereich zu laden.

### Repository hinzufügen & pushen
***
Um die Dokumentation lokal mit Visual Studio Code zu bearbeiten, arbeite ich folgendermassen:

1. Änderungen am Readme-File von meinem Repositorys vornehmen
2. Datei speichern und in der linken Leiste das Symbol mit einer "1" aufrufen
3. Unter dem Abschnitt **Changes** die betroffenen Files bezüglich ihres Changes "stagen"
4. Nachricht hinterlegen und Haken setzen
5. Bei den 3 Punkten (...) die Funktion **Push** aufrufen
6. Warten, bis Dateien vollständig gepusht wurden

## Git-Client
> [⇧ **Nach oben**](#inhaltsverzeichnis)

Damit ich die Arbeiten lokal auf dem eigenen PC machen konnte, musste ich der sogenannte "Git Client", auf Windows "Git/Bash" installieren. 

### Client installieren
***
Ich habe Client-Installation auf [dieser](https://git-scm.com/downloads) Seite heruntergeladen und GUI-basiert installiert.

### Client konfigurieren
***
1. Terminal öffnen
2. Git konfigurieren mit Informationen des GitHub-Accounts:
    ```Shell
      $ git config --global user.name "<username>"
      $ git config --global user.email "<e-mail>"
    ``` 

### Repository herunterladen & aktualisieren (clone/pull)
***
Damit ich das readme-File lokal bearbeiten kann, habe ich das Repository heruntergeladen und aktualisiert.

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
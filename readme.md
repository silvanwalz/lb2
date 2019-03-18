# M300 - LB2 Dokumentation Silvan Walz

Die nachstehende Dokumentation zeigt alle Schritte auf, die ich während der LB2 gemacht habe.

### Inhaltsverzeichnis

* 01 - [VirtualBox](#01---virtualbox)
* 02 - [Vagrant](#02---vagrant)
* 03 - [Visual Studio Code](#03---visual-studio-code)


___

01 - VirtualBox
======

> [⇧ **Nach oben**](#inhaltsverzeichnis)

Als erstes habe ich VirtualBox installiert. 

Dazu habe ich folgende Arbeiten gemacht:

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


02 - Vagrant
======

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
2. In gewünschtem Verzeichnis einen neuen Ordner für die VM anlegen:
    ```Shell
      $ cd Wohin\auch\immer
      $ mkdir MeineVagrantVM
      $ cd MeineVagrantVM
    ``` 
3. Vagrantfile erzeugen, VM erstellen und entsprechend starten:
    ```Shell
      $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Netzwerkshare hinzufügen, falls nicht vorhanden
      $ vagrant init ubuntu/xenial64                                                      #Vagrantfile erzeugen
      $ vagrant up --provider virtualbox                                                  #Virtuelle Maschine erstellen & starten
    ``` 
4. Die VM ist nun in Betrieb (erscheint auch in der Übersicht innerhalb von VirtualBox) und kann via SSH-Zugriff bedient werden:
    ```Shell
      $ cd Pfad\zu\meiner\Vagrant-VM      #Zum Verzeichnis der VM wechseln
      $ vagrant ssh                       #SSH-Verbindung zur VM aufbauen

      #Anschliessend können ganz normale Bash-Befehle abgesetzt werden:

      $ ls -l /bin  #Bin-Verzeichnis anzeigen
      $ df -h       #Freier Festplattenspeicher
      $ free -m     #Freier Arbeitsspeicher
    ``` 
5. VM über VirtualBox-GUI ausschalten

Schlussfolgerung: Keine erheblichen Unterschiede zum ersten Teil (ohne Share) und daher auch nicht wirklich kompliziert.

### Apache Webserver automatisiert aufsetzen
***
Um den Automatisierungsgrad von Vagrant im Rahmen dieser Dokumentation etwas besser hervorzuheben, richten wir eine VM, dass sie direkt mit einem vorinstallierten Apache-Webserver startet. Dazu können wir im Vagrantfile den Code etwas leicht abändern und direkt auf Bash-Ebene mit einfachen Befehlen arbeiten. 

Nachfolgend wird die VM mit einem bereits abgeänderten File bzw. VM aus dem M300-Repository erstellt:

1. Terminal öffnen
2. In das M300-Verzeichnis (\M300\vagrant\web) wechseln:
    ```Shell
      $ cd Pfad/zum-M300-Verzeichnis/vagrant/web
    ``` 
3. VM erstellen und starten:
    ```Shell
      $ vagrant up
    ``` 
4. Webbrowser öffnen und prüfen, ob der Standard-Content des Webservers unter "http://127.0.0.01:8080" (localhost) erreichbar ist
5. Im Ordner `\web` die Hauptseite `index.html` editieren bzw. durch eine andere ersetzen (z.B. HTML5up-Themplate) und das Resultat überprüfen
6. Abschliessend kann die VM wieder gelöscht werden:
    ```Shell
      $ vagrant destroy -f
    ```
7. Vagrant ist nun komplett einsatzfähig!


03 - Visual Studio Code
======

> [⇧ **Nach oben**](#inhaltsverzeichnis)

Bis hierhin haben wir soweit alles aufgesetzt und installiert. Nun möchten wir für effizienteres Arbeiten eine "Entwicklungsumgebung" aufbauen, die es uns ermöglicht, alle lokalen Repositories an einem Ort zu verwalten und die dazugehörigen Dateien zu bearbeiten. Die Lösung hierzu ist: Visual Studio Code 
Dieser freie Quelltext-Editor von Microsoft, ermöglicht uns, unsere Workflows besser zu gestalten und damit die Arbeit um einiges leichter zu machen.

Für die Einrichtung muss man sich nach den nachfolgenden Anweisungen orientieren:

### Software herunterladen & installieren
***
1. Unter [dieser Webseite](https://code.visualstudio.com/"visualstudio.com") lässt sich der Installer (Version 1.26.1) herunterladen.
2. Auf "Download for Mac" klicken und warten, bis das Fenster zum Herunterladen erscheint. Anschliessend den Download des Installers starten
3. Die Installation erfolgt auch hier GUI-basiert. Wiederum aber Standard (ohne spezielle Anpassungen), sodass an dieser Stelle auf eine Erklärung ebenfalls verzichtet wird.
4. Sobald der Vorgang abgeschlossen wurde, kann mit dem Herunterladen der ISO-Datei und der VM-Erstellung fortgefahren werden.


### Extensions installieren
***

Wir fügen dem Editor drei wichtige Extensions hinzu:

* Markdown All in One (von Yu Zhang)
* Vagrant Extension (von Marco Stanzi)
* vscode-pdf Extension (von tomiko1207)

Dazu müssen folgende Anweisungen befolgt werden: 

1. Visual Studio Code öffnen
2. Die Tastenkombination `CTRL` + `SHIFT` + `X` drücken und in der Suchleiste die erwähnten Extensions suchen
3. Auf `Install` klicken und anschliessend auf `Reload`, um die Extension in den Arbeitsbereich zu laden.
4. Nun können die Extensions angewendet werden. Für Markdown ist [diese Liste](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet/"github.com") sehr hilfreich.


### Einstellungen anpassen
***
Damit keine Dateien der virtuellen Maschinen dem Cloud-Repository hinzugefügt werden (da Dateien zu gross), müssen diese in den Einstellungen "exkludiert" werden:

1. Visual Studio Code öffnen
2. Unter `Code` > `Preferences` > `Settings` bei den 3 Punkten (...) auf `Open setting.json` klicken
3. Zu diesem Abschnitt gehen:
     ```
      // Configure glob patterns for excluding files and folders. For example, the files 
      explorer decides which files and folders to show or hide based on this setting. 
      Read more about glob patterns here. (...)
    ``` 
4. Nachstehenden Code einfügen:
     ```
      // Konfiguriert die Globmuster zum Ausschließen von Dateien und Ordnern.
      "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/.vagrant": true,
        "**/.DS_Store": true
      },
    ```
5. Änderungen speichern und die Einstellungen schliessen
   
Nun sollten keine Dateien mit den Endungen .git / .svn / .hg / .vagrant / .DS_store hochgeladen werden. Wie man die Änderungen innerhalb von Visual Studio Code richtig pusht, wird im nachfolgenden Abschnitt erklärt. 

### Repository hinzufügen & pushen
***
1. Visual Studio Code öffnen
2. Änderungen an entsprechenden Dateien des lokalen Repositorys vornehmen
3. In der linken Leiste das Symbol mit einer "1" aufrufen
4. Unter dem Abschnitt **Changes** die betroffenen Files bezüglich ihres Changes "stagen" (**Stage Changes**)
5. Nachricht hinterlegen (**Message**) und Haken (**Commit**) setzen
6. Bei den 3 Punkten (...) die Funktion **Push** aufrufen
7. Warten, bis Dateien vollständig gepusht wurden
___

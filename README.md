# Keil Linux Anleitung

Dies ist eine Anleitung, wie man Keil auf Linux installiert.

Getestet unter Arch Linux und Lubuntu
(sollte auf anderen Distributionen auch funktionieren, ggf.
heißen die zu installierenden Pakete anders)

## Funktionen

**Funktionert:**

- Code kompilieren
- Programm auf das ITSBoard hochladen

**Funktioniert nicht:**

- Keil Debugger (da ST-Link als externes Programm verwendet wird)

## Schritt 1: Notwendige Pakete installieren

`wine` und `st-link` über den Paketmanager installieren.

Je nach Distribution:

`sudo pacman -Syu wine stlink`

`sudo apt-get install wine stlink-tools`

[etc.]

## Schritt 2: Keil herunterladen

Von Dropbox `Keil_v5.zip` herunterladen und entpacken.

Link: [https://www.dropbox.com/s/ditsd04i56gsmvq/Keil_v5.zip?dl=1](https://www.dropbox.com/s/ditsd04i56gsmvq/Keil_v5.zip?dl=1)

## Schritt 3: Keil starten und beten

Es ist kein Virus, versprochen ;)

`wine Keil_v5/UV4/UV4.exe`

Jetzt sollte Keil starten.

Wenn man Keil bequem starten möchte, kann man sich ein Shellscript machen
und einen Symlink nach `/usr/bin/` erstellen

z.B.

**keil.sh**

    #!/bin/sh
    wine Keil_v5/UV4/UV4.exe

`sudo ln -s keil.sh /usr/bin/keil`

## Schritt 4: Projekt testen

Jetzt sollte man mit Keil bereits Projekte öffnen und Kompilieren können.

Damit man das Hochladen auf das Board auch funktioniert

Menüpunkt `Flash -> Configure Flash Tools` auswählen.

Im Tab `Output` die Checkbox `Create HEX File` auswählen-
Im Tab `Utilities` den Radiobutton `Use External Tool for Programming` auswählen.
Im Textfelld `Command` folgendes eintragen `/usr/bin/st-flash --format ihex write ITSboard.hex`

**Im Repository ist auch ein Beispielprojekt was bereits richtig eingestellt ist**

`example.zip` entpacken (Ist ein Demo-Programm)

# Keil Linux Anleitung

Getestet unter Arch Linux und Lubuntu
(sollte auf anderen Distributionen auch funktionieren, ggf.
heißen die zu installierenden Pakete anders)

## Funktionen

**Funktionert:**

- Code kompilieren
- Programm auf das ITSBoard hochladen

**Funktioniert nicht:**

- Debugger (da ST-Link als externes Programm verwendet wird)

## Schritt 1: Notwendige Pakete installieren

`wine` und `stlink` über den Paketmanager installieren.

Je nach Distribution:

`sudo pacman -Syu wine stlink`

`sudo apt install wine stlink-tools`

[etc.]

## Schritt 2: Keil herunterladen

Von meiner Dropbox [Keil_v5.zip](https://www.dropbox.com/s/ditsd04i56gsmvq/Keil_v5.zip?dl=1) herunterladen und entpacken. (Ist eine vorbereitete Keil-Version, die ohne Installation funktioniert)

`unzip ~/Downloads/Keil_v5.zip`

Den Ordner nach `~/.wine/drive_c/` verschieben:

`mv Keil_v5/ ~/.wine/drive_c/`

## Schritt 3: Keil starten

Mit folgendem Befehl Keil starten:

`wine ~/.wine/drive_c/Keil_v5/UV4/UV4.exe`

Wenn man Keil bequem starten möchte, kann man sich ein Shellscript machen
und einen Symlink nach `/usr/bin/` erstellen

**keil.sh**

    #!/bin/sh
    wine ~/.wine/drive_c/Keil_v5/UV4/UV4.exe

`sudo ln -s keil.sh /usr/bin/keil`

## Schritt 4: Upload auf Board

Damit man das Hochladen auf das Board auch funktioniert:

Menüpunkt `Flash -> Configure Flash Tools` auswählen.

Im Tab `Output` die Checkbox `Create HEX File` setzen.

Im Tab `Utilities` den Radiobutton `Use External Tool for Programming` setzen.

Checkbox `Run Independent` setzen.

Im Textfeld `Command` eintragen: `/usr/bin/st-flash --format ihex write ITSboard/ITSboard.hex`

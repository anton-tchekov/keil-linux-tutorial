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

`sudo apt install wine stlink-tools`

[etc.]

## Schritt 2: Keil herunterladen

Von meiner Dropbox [Keil_v5.zip](https://www.dropbox.com/s/ditsd04i56gsmvq/Keil_v5.zip?dl=1) herunterladen und entpacken. (Ist eine vorbereitete Version, die out-of-the-box ohne Installation funktioniert)

Ist kein Virus, versprochen ;)

## Schritt 3: Keil starten und beten

Mit folgendem Befehl Keil starten:

`wine Keil_v5/UV4/UV4.exe`

Wenn man Keil bequem starten möchte, kann man sich ein Shellscript machen
und einen Symlink nach `/usr/bin/` erstellen

z.B.

**keil.sh**

```
    #!/bin/sh
    wine Keil_v5/UV4/UV4.exe
```

`sudo ln -s keil.sh /usr/bin/keil`

Dann muss man im Pack Installer von Keil (Grünes Icon im Toolbar, zweite Reihe ganz rechts)
zwei Pakete installieren: `Keil::STM32F4xx_DSP` und `ARM::CMSIS`

## Schritt 4: Upload auf Board

Damit man das Hochladen auf das Board auch funktioniert:

Menüpunkt `Flash -> Configure Flash Tools` auswählen.

Im Tab `Output` die Checkbox `Create HEX File` setzen.

Im Tab `Utilities` den Radiobutton `Use External Tool for Programming` setzen.

Im Textfelld `Command` folgendes eintragen `/usr/bin/st-flash --format ihex write ITSboard.hex`


## Test

https://www.dropbox.com/s/zaivxrvrgk2cxvi/praktikum.zip?dl=1

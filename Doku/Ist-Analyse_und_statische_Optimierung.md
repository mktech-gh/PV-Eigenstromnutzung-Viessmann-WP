# Viessmann Wärmepumpen-Heizung mit Pufferspeicher optimieren für Betrieb mit PV-Anlage

## Ausgangslage

Die Heizungsanlage wurde im Januar 2023 installiert und in Betrieb genommen. Der Wärmepumpen-Vorlauf wird oben in einen Pufferspeicher geleitet und verlässt diesen ebenfalls oben in die FBHeizung. Der Rücklauf aus der FBHeizung wird unten in den Pufferspeicher geleitet und fliesst ebenfalls unten in die Wärmepumpe.

Die Wärmepumpe wird mit folgenden Parametern betrieben:
- 00:00 bis 24:00 Reduzierter Betrieb mit Zieltemperatur 18Grad
- 05:00 bis 22:00 Normalbetrieb mit Zieltemperatur 21Grad
Heizkurve:
  - Niveau 0 (Bedutet bei Zieltemperatur 21Grad und Aussentemperatur von 0Grad eine Vorlauftemperatur von 33Grad)
  - Neigung 0.4

### Feststellungen

- Der Pufferspeicher macht nur Sinn, wenn eine intelligente Kopplung mit der PV-Anlage besteht. Ohne Kopplung ist der Pufferspeicher (meine pers. Meinung) kontraproduktiv:
  - Der Pufferspeicher muss am Morgen zuerst aufgewärmt werden bis die gewünschte Puffer-Vorlaufttemperatrur erreicht wird und bis sich die Differenz zwischen Wärmepumpen-Rücklauf (aus dem Pufferspeicher) und dem Wärmepumpen-Vorlauf auf die betriebsdifferenz von 2 bis 4 Grad eingependelt ist. 
  - Diese "Verlust"-Energie könnte eventuell am Abend zum Teil mit einer früheren Umstellung auf reduzierten Betrieb, kompensiert werden.
- Ein intelligente Kopplung ist nur mit einer Viessmann-PV-Anlage möglich.
- Reduzierter Nachtbetrieb;
  - Bei der Umschaltung von normalem auf reduziertem Betrieb wird der Verdichter manchmal abgeschaltet. Von Tag zu Tag unterschiedlich. 
  - Wenn der verdichter nicht abgeschaltet wird, kann eine um ca. 3 Grad reduzierte Vorlauftemperatur festgestellt werden. 
  - Wird der Verdichter bei Umschaltung auf reduzierten Betrieb abgeschalten, dann fällt die Vorlauftemperatur langsam innerhalb von 6h auf 23Grad.
  - Nach diesem Abfall schaltet der Verdichter noch vor der Umschaltung auf Normalbetrieb wieder ein. Annahme: Die Vorlauftemperatur (noch aus den Reserven des Pufferspeichers) sinkt unter einen bestimmten Vorlaufwert.
  - Temperaturen wenn Verdichter abgeschaltet wird (14.Feb.23 00:00/03:00Uhr): 
    - Speicher-Top: 27.6/24.4
    - Heizungssystem-Rücklauf: 27.5/24.3
    - Wärmepumpen-Vorlauf: 26.7/23.6
    - Da der Rücklauf höher als der Vorlauf ist, kann festgehalten werden: 
      - Der Vorlauf wird gemischt mit dem Speicher in das Heizungsystem eingespiesen. Die Speicherwärme wird somit durch den Betrieb mit der Umwälzpumpe genutzt.

### Informationen
- Viessmann Funktion Pufferspeicher: https://www.viessmann.ch/de/wissen/technik-und-systeme/heizwasser-pufferspeicher.html
- [pr-speicher-wassererwaermer_vitocell.pdf](https://github.com/mktech-gh/SmartHome-and-IoT/files/10737146/pr-speicher-wassererwaermer_vitocell.pdf)

### Projektziel

1. Optimierungen gemäss Seite 14 der Bedienungsanleitung 
-    [Vitotronic 200Bedienungsanleitung.pdf](https://github.com/mktech-gh/SmartHome-and-IoT/files/10737513/Vitotronic.200Bedienungsanleitung.pdf)
2. Optimierung der Heizzeiten um die Pufferwärme für reduzierung des Einspeise-Energieverbrauchs zu nutzen
3. Mit einer eigenen intelligenten Kopplung soll der Nutzen des Pufferspeichers genutzt werden. Analog Smard Grid - Steuerung gemäss Bedienungsanleitung Seite 50 und 101 
4. eine verfrühte Einschaltung des Verdichters am frühen Morgen ist entgegenzuwirken. Dabei wird in erster Linie der Puffer aufgeheizt.



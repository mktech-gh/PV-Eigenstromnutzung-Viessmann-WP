# Ist-Analyse_und_statische_Optimierung

## Ausgangslage

Die Heizungsanlage wurde im Januar 2023 installiert und in Betrieb genommen. Der Wärmepumpen-Vorlauf ist direkt mit dem Heizkreis und dem Pufferspeicher (oben) verbunden. Der Rücklauf aus der FBHeizung wird unten in den Pufferspeicher geleitet und fliesst ebenfalls unten in die Wärmepumpe. Der Pufferspeicher wirkt als eine [Hydraulische Weiche] (https://de.wikipedia.org/wiki/Hydraulische_Weiche).

Die Wärmepumpe wird mit folgenden Parametern betrieben:
- 00:00 bis 24:00 Reduzierter Betrieb mit Zieltemperatur 18Grad
- 05:00 bis 22:00 Normalbetrieb mit Zieltemperatur 21Grad
Heizkurve:
  - Niveau 0 (Bedutet bei Zieltemperatur 21Grad und Aussentemperatur von 0Grad eine Vorlauftemperatur von 33Grad)
  - Neigung 0.4
- Temperaturdifferenz für Berechnung der Heizgrenze 7003: 4K (entspricht einer Temperatur von 21 + 4 = 17K)
- Temperaturdifferenz für Berechnung der Kühlgrenze 7004: 4K (entspricht einer Temperatur von 21 + 4 = 25K)

### Feststellungen

- Der Pufferspeicher macht nur Sinn, wenn eine intelligente Kopplung mit der PV-Anlage besteht. Ohne Kopplung ist der Pufferspeicher (meine pers. Meinung) kontraproduktiv:
  - Der Pufferspeicher muss am Morgen zuerst aufgewärmt werden bis die gewünschte Puffer-Vorlaufttemperatrur erreicht wird und bis sich die Differenz zwischen Wärmepumpen-Rücklauf (aus dem Pufferspeicher) und dem Wärmepumpen-Vorlauf auf die betriebsdifferenz von 2 bis 4 Grad eingependelt ist.
  - Diese "Verlust"-Energie könnte eventuell am Abend zum Teil mit einer früheren Umstellung auf reduzierten Betrieb, kompensiert werden.
  - Wirth meint, dass der Pufferspeicher verhindert, dass der Verdichter am Morgen zu viele Start/Stops hat. Ich bezweifle das eine so grosse Dimensionierung notwendig ist. Eine normale hydraulische Weiche in Rohr-Ausführung hätte gereicht. Ev. wird der Pufferspeicher im Kühlbetrieb einen Vorteil bringen.
  - Ein intelligente Kopplung ist nur mit einer Viessmann-PV-Anlage möglich.
- Reduzierter Nachtbetrieb;
  - Bei der Umschaltung von normalem auf reduziertem Betrieb wird der Verdichter manchmal abgeschaltet. Von Tag zu Tag unterschiedlich. 
  - Wenn der verdichter nicht abgeschaltet wird, kann eine um ca. 3 Grad reduzierte Vorlauftemperatur festgestellt werden. 
  - Wird der Verdichter bei Umschaltung auf reduzierten Betrieb abgeschalten, dann fällt die Vorlauftemperatur langsam innerhalb von 6h auf 23Grad.
  - Die folgende Fesstellung basiert eventuell auf der ungünstigen Wahl der Betriebs-Modi/Zeiten:
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

### Vorgehen

__1. Optimierungen__ 
- Inspiration: Seite 14 der Bedienungsanleitung [Vitotronic 200Bedienungsanleitung.pdf](https://github.com/mktech-gh/SmartHome-and-IoT/files/10737513/Vitotronic.200Bedienungsanleitung.pdf)
  a. 20230221
  - Reduktion des Heizkurven-Niveaus von 0 auf -2
  - 00:00 "Standby" (Keine Betriebsart ausgelesen)
  - 05:00 "Normal" - Betrieb auf 21C
  - 21:00 "Reduziert" - Betrieb auf 17C
    - Durch den reduzierten Betrieb bleibt die Umwälzpumpe eingeschaltet und die Pufferenergie wird auf die Fussbodenheizung übertragen.
    - Durch die Senkung der Temperatur beim "reduzierten Betrieb" sollte keine Einschaltung des Verdichters vor der Umschaltung auf "Normal-Betrieb" erfolgen.
    - Der Verdichter-Vorlauf wird im reduzierten Betrieb auf Aussentemperatur abgekühlt. Dadurch wird auch das gesamte System auf Aussenthemperatur abgekühlt. Mit dem Standby-Betrieb (Umwälzpumpe aus) soll ab 00:00 eine weitere Abkühlung des Puffers verhindert werden. Die Themperatur ist dann etwa uaf Raumtemperatur.
  - Temperaturdifferenz für Berechnung der Heizgrenze 7003: 4K (entspricht einer Temperatur von 21 + 4 = 17K)
  - Temperaturdifferenz für Berechnung der Kühlgrenze 7004: 4K (entspricht einer Temperatur von 21 + 4 = 25K) 

 - __Ergebnis:__
  
    - Normal Betrieb
      - In den Temperaturaufzeichnungen kann festgestellt werden, dass um 05:00 der Verdichter wie gewünscht einschaltet und die Temperatur korrekt auf die HK0_Zieltemperatur einstellt. Je nach Aussentemperatur kann dann folgendes Verhalten festgestellt werden:
      
        - Aussentemperatur ist so warm, dass die benötigte Heizenergie kleiner als die minimale Heizenergie der WP ist
          - Die Vorlauftemperatur driftet nach oben ab. Wird ein bestimmtes Kriterium erreicht, stellt der Verdichter ab.
          - ![20230224 Viessmann 200-A 24h Heizen mit Verdichterausschaltung Standby ](https://user-images.githubusercontent.com/102212594/221433771-465104e4-09b7-4b4b-aebf-3aa217598dd5.png)
          - Die WP kann je nach Energiebedarf (Aussenthemperatur/Rücklauf usw) den Verdichter nochmals starten
          - Spätestens mit der Umschaltung auf "Reduzierten"-Betrieb (21:00) wird eine Einschaltung des Verdichters von der WP noch einmal in Erwägung gezogen. Auf jeden Fall läuft die Umwelzpumpe nach dem Ausschalten des Verdichters und der Umschaltung iim "reduzierten" Betrieb weiter.
      
        - Die Aussentemperatur so kalt ist, dass mehr als die minimale Leistung der WP benötigt wird:
          - Die WP regelt genau auf die gewünschte HK0_Zieltemperatur.
          - ![20230225 Viessmann 200-A 24h Heizen Warmwasser Standby  ](https://user-images.githubusercontent.com/102212594/221435098-3bc5c98e-79bc-4266-9a65-7d2ae610f6ca.png)
        
    - Reduzierter Betrieb
      - Im Reduzierten Berieb kann keine temperaturabhängige Aktion festgestellt werden. Die Umwälzpumpe ist in Betrieb und verteilt den Pufferinhalt. Es ist zu erwarten, dass bei ganz tiefen Temperaturen der Verdichter eingeschalten wird.
      
    - Standby Betrieb
      - Im Standby Betreib sind Verdichter und Umwälzpumpe ausgeschalten. 
      - Fällt die Aussentemperatur unter 3Grad, so wird der Frostschutz aktiv und die Umwälzpumpe wird mit einer HK0_Zieltemperatur von 15 Grad aktiviert
      - ![20230226 Viessmann 200-A 24h Heizen Standby Frostschutz ](https://user-images.githubusercontent.com/102212594/221435357-e3aa56ed-d3d5-4e73-9961-06e1bcae5b95.png)
   

2. Optimierung der Heizzeiten um die Pufferwärme für reduzierung des Einspeise-Energieverbrauchs zu nutzen
3. Mit einer eigenen intelligenten Kopplung soll der Nutzen des Pufferspeichers genutzt werden. Analog Smard Grid - Steuerung gemäss Bedienungsanleitung Seite 50 und 101 
4. eine verfrühte Einschaltung des Verdichters am frühen Morgen ist entgegenzuwirken. Dabei wird in erster Linie der Puffer aufgeheizt.



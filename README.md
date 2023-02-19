# Viessmann Wärmepumpen-Heizung mit Pufferspeicher optimieren für Betrieb mit PV-Anlage

Optimale Eigenstromnutzung durch smarte Parameterisierung der Viessmann-WP

Ein wirtschaftlicher Betrieb einer PV-Anlage setzt eine möglichst hohen Eigenstromnutzung voraus. Grundsätzlich wiederspricht sich "heizen" und "hohes PV-Energieangebot". Trotzdem soll möglichst viel PV-Eigenstrom für die Wärmepumpe eingesetzt werden.

Im Kühlbetrieb (Sommer) ist der Energiebedarf propotional zum PV-Ertrag und somit ideal für eine PV-Eigenstromnutzung.

## Bei Wärmebedarf den Eigenstromverbrauch optimieren 

Vorgehen:

1. Analyse von Verhalten (Heizkurven, Ein-, Ausschalten usw.) und Einstellungen der Wärmepüumpen-Heizung für ein baselining.
  - [Analyse Heizungsanlage](https://github.com/mktech-gh/SmartHome-and-IoT/blob/main/Doku/Analyse%20Projekt%20Mattes%20Viessmann.md)

2. Datensammlung aller Werte (Temperaturen, Aktivierung/Deaktivierung von Verdichter und Umwälzpumpe usw.) in eine influxDB

2. Konzept für eine Optimierung des Eigenstromverbrauchs

3. HW- und SW-Komponenten

# Velux MQTT-Plugin

Das Plugin **Velux-MQTT** ermöglicht es Ihnen, Ihre Oberlichter in Jeedom über die VELUX KLF 200-Schnittstelle zu steuern und deren Position, Anheben oder Absenken und Stoppen zu steuern.

Die Oberlichter müssen zuerst mit der VELUX KLF 200 Schnittstelle gekoppelt werden und sie muss über Ethernet mit demselben lokalen Netzwerk wie Jeedom verbunden sein *([siehe KLF 200 Dokumentation](https://www.domadoo.fr/fr/index.php?controller=attachment&id_attachment=2287){:target="\_blank"})*.

# Configuration

Wie jedes Jeedom-Plugin ist das plugin **Velux-MQTT** muss nach der Installation aktiviert werden.

## Abhängigkeitsverwaltung

Das Plugin **Velux-MQTT** setzt auf offizielle Plugins **Docker-Verwaltung** und **MQTT-Manager** arbeiten. Wenn dies noch nicht der Fall war, werden diese 2 Plugins während der Installation der Abhängigkeiten installiert.

>**INFORMATION**
>
>Die Installation von Abhängigkeiten kann je nach Konfiguration mehrere Minuten dauern.

## MQTT-Manager

Im Plugin muss ein MQTT-Broker konfiguriert und aktiv sein **MQTT-Manager** um die Positionen der Oberlichter zu übertragen und abzurufen. Lesen Sie die Plugin-Dokumentation, um einen vorhandenen Broker zu verwenden oder einen lokal in Jeedom zu erstellen.

Sobald der Plugin-Daemon **MQTT-Manager** aktiv sein, das Plugin **Velux-MQTT** in der Lage sein, MQTT-Broker-Verbindungsinformationen automatisch abzurufen.

## Plugin-Setup

Die Konfiguration des Plugins besteht aus dem Ausfüllen der Verbindungsinformationen zur VELUX KLF 200-Schnittstelle :

- **IP Adresse** : Die IP-Adresse des KLF200 im lokalen Netzwerk.
- **WLAN Passwort** : Das WLAN-Passwort des KLF200 *(rückseitig beschriftet)*.

## Installieren des Velux MQTT-Containers

Sobald die Verbindungsinformationen für die VELUX KLF 200 Schnittstelle eingegeben und gespeichert wurden, klicken Sie auf die Schaltfläche **Installieren Sie VELUX MQTT** um zu überprüfen, ob alles in Ordnung ist und mit der Erstellung des Containers fortzufahren **Velux-MQTT** im Plugin **Docker-Verwaltung**.

Am Ende des Verfahrens stehen die Statuten des Hafenarbeiters **Velux-MQTT** müssen mit den Wörtern grün dargestellt werden *"running"* und *"CONNECTED"*. Wenn nicht, überprüfen Sie die Geräteprotokolle **Velux-MQTT** im Plugin **Docker-Verwaltung**.

# Equipements

Um auf die verschiedenen Velux-Geräte zuzugreifen, gehen Sie zum Menü **Plugins → Heimautomatisierungsprotokoll → Velux MQTT**.

Die Taste **Zu synchronisieren** ermöglicht es Ihnen, automatisch die Ausrüstung zu erstellen, die den Oberlichtern entspricht, die auf der KLF 200-Schnittstelle in Jeedom aufgelistet sind.

# Commandes

Jedes Gerät **Velux-MQTT** hat diese Befehle :

- **Zustand** : aktuelle Position des Dachfensters.

>**TRICK**
>
>Standardmäßig stellt die KLF 200-Schnittstelle einen Abschlussprozentsatz bereit *(100 % = geschlossen)* dass sich das Plugin in einen offenen Prozentsatz umwandelt. Wenn Sie zum Standardbetrieb zurückkehren möchten, deaktivieren Sie einfach das Kontrollkästchen **Umkehren** der Bestellung **Zustand**.

- **Position** : Steuerung der Oberlichtpositionierung.
- **Offen** : Befehl zum Öffnen des Dachfensters.
- **Stoppen** : Befehl zum Stoppen des Oberlichts.
- **Nah dran** : Befehl zum Schließen des Dachfensters.
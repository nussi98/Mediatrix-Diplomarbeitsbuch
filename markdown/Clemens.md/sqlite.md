Als Datenbank wurde in diesem Projekt SQLite gewählt.
Bei SQLite handelt es sich um eine Datei-basierte Datenbank,
das bedeutet, dass im Hintergrund eine C-Library arbeitet
und die Daten in einem File im Dateisystem ablegt.
Im Vergleich zu anderen Datenbanksystemen wie MySql
ist hier kein zusätzlicher Datenbank-Server notwendig.
Der Zugriff auf die Datenbank ist - wie bei anderen Datenbanken - mit SQL möglich.
Ein Problem von SQLite ist, dass bei jedem Schreibvorgang die gesamte Datenbank-Datei neu geschrieben wird.
Somit ist das Einfügen von Daten in die Datenbank sehr langsam.
Weiters sollte auch beachtet werden, dass Dateien auf dem Webserver meist öffentlich einsehbar sind.
Das sollte bei SQlite zumindest für das Datenbankverzeichnis verhindert werden,
da sonst die gesamte Datenbank von einem Client heruntergeladen werden kann.
Ein Vorteil hingegen entsteht beim Lesen von Daten.
Da im Hintergrund keine Verbindung hergestellt werden muss,
ist der Lesevorgang schneller als bei herkömmlichen Datenbanken. \cite[S. 617]{wenz_php_2017}

## Vorteile für diese Projekt
SQLite bringt für dieses Projekt einen großen Vorteil, da die Datenbank als Datei abgelegt werden kann
und kein eigener Datenbank-Server betrieben werden muss.
Das bringt eine Reduktion der verwendeten Ressourcen, 
die durch den Raspberry Pi nur sehr knapp zur Verfügung stehen.
Weiters finden auch sehr selten Schreibzugriffe statt, 
weswegen die etwas langsamere Geschwindigkeit hierbei keine Rolle spielt.
Ein Vorteil gegenüber eines einfachen JSON-Files, in das die Daten abgespeichert werden, ist,
dass auch Relationen abgebildet werden können.

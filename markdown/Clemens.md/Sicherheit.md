Die Sicherheit spielt in diesem Projekt natürlich eine zentrale Rolle. 
Dafür wurde auf Ebene des Betriebssystems der Fokus auf verschlüsselte Verbindungen und eine Firewall gelegt.

## SSL und TLS
SSL \bzw TLS (im Weiteren als SSL bezeichnet) wurde in diesem Projekt durch 
HTTPS (Hypertext Transfer Protokoll Secure) und WSS (Websocket Secure) integriert.

SSL (Secure Sockets Layer) beschreibt ein Verfahren,
bei dem unsichere Protokolle wie HTTP  (Hypertext Transfer Protokoll) und WS (Websocket) in eine verschlüsselte Kommunikation eingebettet werden 
und weiters auch eine Authentifizierung von Server und Client möglich ist. Das Verfahren arbeitet mit 
öffentlichen und privaten Schlüsseln. Das Prinzip der Schlüsselpaare funktioniert folgendermaßen:
Wollen zwei oder mehrere Geräte miteinander über ein öffentliches Netz verschlüsselt kommunizieren, 
erstellt sich jeder Teilnehmer ein Schlüsselpaar, bestehend aus einem privaten und einem öffentlichen Schlüssel.
Will nun ein Gerät mit dem Server verschlüssselt kommunizieren, wird ihm vom Server sein öffentlicher Schlüssel zugeschickt. 
Alle weiteren Nachrichten werden mit diesem öffentlichen Schlüssel verschlüsselt.
Die Nachrichten, die gesendet werden, sind nun nicht mehr lesbar und 
können nur mit dem privaten Schlüssel vom Server entschlüsselt werden.
Um die Authentifizierung des Servers zu gewährleisten, sollten die öffentlichen Schlüssel (Zertifikate) von einer
offiziellen Stelle beglaubigt werden. \cite[S. 675 ff.]{wenz_php_2017}

## Firewall

\begin{quote}
    „Eine Paketfilter-Firewall analysiert den Datenverkehr im Netzwerk, indem sie die Header der Pakete betrachtet. 
    Anhand von festgelegten Filterregeln wird entschieden, ob ein Paket geblockt und verworfen wird oder seinen Weg fortsetzen darf.“ \cite[S. 715]{jurzik_debian_2013}
\end{quote}

In Linux wird bereits eine Firewall namens Netfilter/IPTables mit ausgeliefert. 
Während Netfilter die Kernel-Komponente, die die Filterung vornimmt, darstellt, 
ist IPTables das Programm, das diese steuert.

Die Konfiguration von IPTables gliedert sich in Tabellen und Listen. Generell können die Tabellen *filter*, 
*nat* und *mangle* bearbeitet werden. 
Die beiden Letzteren sind für die Grundfunktion der Firewall nicht notwendig 
und werden deshalb auch nicht weiter ausgeführt.
Jede Tabelle enthält Listen, in denen Regeln stehen, wie Pakete behandelt werden sollen.
Die Regeln werden nacheinander abgearbeitet und sobald eine Regel zutrifft, wird keine weitere mehr angewandt.
Die *filter*-Tabelle gliedert sich in drei vordefinierte Listen: INPUT, OUTPUT und FORWARD.

* INPUT ist eine Liste von Regeln, die bei ankommenden Paketen angewandt werden. 
* Die Regeln der Liste OUTPUT werden bei ausgehenden Paketen verwendet.
* FORWARD wird zusätzlich angewandt, wenn der Server als Router fungiert. 

Um das Verwalten der Firewall zu vereinfachen, wurde in diesem Projekt ufw (Uncomplicated Firewall) verwendet.
Ufw ist ein Programm, das ein Kommandozeilen-Programm für die Erstellung von Regeln für IPTables bereitstellt. \cite{noauthor_uncomplicated_nodate}

Es wurden Regeln für die Verwendung von HTTPS, SSH und HTTP erstellt, alle anderen Ports wurden geblockt. (siehe \abb{ufw})

![Die konfigurierten UFW-Regeln\label{ufw}](bilder/Clemens/ufw.png){width=90%}
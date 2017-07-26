---
title: ispCP Omega auf Debian/Ubuntu installieren
author: Benjamin Altpeter
type: post
date: 2012-09-10T10:50:50+00:00
excerpt: In diesem Artikel erkläre ich die Installation des kostenlosen Hosting-Panels ispCP unter Debian/Ubuntu. ispCP stellt u.a. eine cPanel-Alternative dar.
url: /ispcp-auf-debianubuntu-installieren/
categories:
  - Allgemein
  - Text-/Bildtutorials
  - Tipps und Tricks
  - Tutorials
tags:
  - control panel
  - controlpanel
  - cpanel
  - debian
  - free cpanel
  - installation
  - ispcp
  - ispcp omega
  - ubuntu
  - v-server
  - vps

---
### Einleitung

In diesem Tutorial möchte ich euch einmal zeigen, wie ihr das kostenlose Open Source-Hosting Panel ispCP Omega auf Debian oder Ubuntu installieren könnt.
  
Im Grunde genommen ist die Installation recht einfach, trotzdem gibt es einiges zu beachten.

Zu beachten ist, dass ispCP sich nicht auf einem einfachen Webspace-Paket installieren lässt, stattdessen benötigt man einen Server mit vollem Root-Zugriff. Es reicht allerdings auch ein kleiner VPS-Server.

Hier sind die empfohlenen Mindestvorraussetzungen von der Herstellerwebseite, erfahrungsgemäß muss es allerdings nicht einmal so viel sein. Ich habe ispCP z.B. auch auf einem VPS mit 128 MB RAM zum Laufen bekommen&#8230;

  *  Intel Pentium III oder AMD K6-3 mit 500 MHz
  *  256 MB RAM
  *  120 MB Festplattenspeicher (nur für die Installation von ispCP ω)
  *  Debian, Ubuntu, Redhat, FreeBSD oder ein anderes unterstütztes, frisch installiertes Host-System
  *  Internetverbindung

### Installation

  1. Zur Installation brauchen wir ein frisch installiertes Debian oder Ubuntu, es dürfen noch keine Pakete wie Apache etc. installiert sein!
  2. Zunächst loggen wir uns über SSH auf unserem Server ein.
  
    Für einige der Schritte benötigen wir Root-Rechte. Diese erhalten wir beispielsweise mit dem Befehl</p> <pre lang="bash">sudo -i</pre>

  3. Damit alle Schritte ausgeführt werden können, brauchen wir drei Pakete, die wahrscheinlich bereits installiert sind. Trotzdem führen wir zur Sicherheit folgenden Befehl aus: <pre lang="bash">apt-get install wget unzip aptitude</pre>

  4. Nun wechseln wir in das Verzeichnis, in welchem wir die temporären Dateien speichern. Ich verwende dafür /usr/local/src: <pre lang="bash">cd /usr/local/src</pre>

  5. In dieses Verzeichnis laden wir ispCP nun herunter. Die jeweils aktuellste Version findet ihr immer unter <a title="ispCP-Download" href="http://isp-control.net/downloads-2/" rel="nofollow">http://isp-control.net/downloads-2/</a>. Zu Zeitpunkt dieses Artikel ist die 1.1.0 Beta 1 die neuste. Also lade ich diese herunter: <pre lang="bash">wget http://downloads.sourceforge.net/project/ispcp/ispCP%20Omega/ispCP%20Omega%201.1.0%20Beta%201/ispcp-omega-1.1.0-beta1.zip</pre>

  6. Natürlich muss dieses Archiv entpackt werden. Danach welches wir in das erstellte Verzeichnis&#8230; <pre lang="bash">unzip ispcp-omega-1.1.0-beta1.zip
cd  ispcp-omega-1.1.0-beta1</pre>

  7. Wir bringen unser System auf den neusten Stand und installieren das Paket _lsb-release_, welches wir später noch brauchen werden&#8230; <pre lang="bash">aptitude update && aptitude safe-upgrade
aptitude install lsb-release</pre>

  8. Je nachdem, welches Host-System wir verwenden wechseln wir ins Verzeichnis _docs/Debian_ oder _docs/Ubuntu_. <pre lang="bash">cd docs/Ubuntu</pre>

  9. Damit ispCP funktioniert, werden diverse Pakete wie Apache oder MySQL benötigt. Diese installieren wir automatisch mit folgendem Befehl. Auch hier ist wichtig, dass wir die richtige Distribution (Debian oder Ubuntu) einsetzen. <pre lang="bash">aptitude install $(cat ./ubuntu-packages-`lsb_release -cs`)</pre>
    
    Während dieser Installation werden wir nun nach einigen Angaben gefragt, diese geben wir wie folgt an:
    
      * Bei der Installation des MySQL-Servers muss ein Root-Passwort angegeben werden. Hier sollten wir ein sicheres Passwort angeben, das wir uns aber trotzdem merken!
      * Courier darf nicht für Webverzeichnisse installiert werden.
      * Postfix wird für &#8222;internet site&#8220; installiert.
      * Und schließlich wird ProFTPd &#8222;Standalone&#8220; installiert.
 10. Wir wechseln wieder zurück in unser Hauptverzeichnis <pre lang="bash">cd ../..</pre>

 11. Dies ist der erste Schritt, der sich bei Debian oder Ubuntu wirklich unterscheidet. Um nun die Installation zu starten, nutzen wir bei Debian einfach den Befehl <pre lang="bash">make install</pre>
    
    Ubuntu-Nutzer hingegen geben folgenden Befehl ein:
    
    <pre lang="bash">make -f Makefile.ubuntu install</pre>

 12. Nach der Installation kopieren wir die zunächst temporär geschrieben Dateien ins Root-Verzeichnis: <pre lang="bash">cp -Rv /tmp/ispcp/* /</pre>

 13. Und zu guter Letzt starten wir die Einrichtung <pre lang="bash">cd /var/www/ispcp/engine/setup
perl ispcp-setup</pre>

 14. Die Installation ist von nun an selbst erklärend.
  
    Danach können wir unser ispCP im Browser über die während das Setups angegeben Adresse aufrufen.

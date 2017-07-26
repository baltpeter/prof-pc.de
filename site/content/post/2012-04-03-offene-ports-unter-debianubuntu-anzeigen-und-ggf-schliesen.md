---
title: Offene Ports unter Debian/Ubuntu anzeigen und ggf. schließen
author: Benjamin Altpeter
type: post
date: 2012-04-03T17:07:15+00:00
excerpt: Wie zeigt man unter Debian/Ubuntu Ports anzeigt und ggf. schließt...
url: /offene-ports-unter-debianubuntu-anzeigen-und-ggf-schliesen/
categories:
  - Allgemein
tags:
  - debian
  - linux
  - offen
  - offene ports anzeigen
  - offene ports schließen unter ubuntu
  - ports
  - schließen
  - ubuntu

---
Wieder mal das alte Szenario: Ich denke mir, dass ich einen Befehl oder Sonstiges öfter brauchen werde, bin mir aber sicher, dass ich ihn mir nicht merken werde. Also folgt &#8211; schwupdiwups &#8211; ein Artikel.

So ist es auch heute. Wollte auf einer Ubuntu-Maschine, auf der bisher Apache lief mal nginx ausprobieren, also schnell

<pre>apt-get remove apache2</pre>

und mit der Installation von nginx beginnen (Tutorial folgt&#8230;). Nach der Einrichtung Browser öffnen, IP des Rechners eingeben und &#8222;WTF!&#8220; schreien:

> ## Not Found
> 
> The requested URL / was not found on this server.
> 
> * * *
> 
> <address>
>   <span style="color: #ff0000;">Apache</span> Server at [PUTRANDOMIPINHERE] Port 80
> </address>

In so einem Fall braucht man den folgenden Befehl:

`netstat --tcp -p -a`

Daraufhin wird man etwas sehen, das dem folgenden ähnelt:

{{< img src="/uploads/2012/04/netstat.png" caption="Mit netstat offene Ports anzeigen" >}}

Und wie wir sehen: Auf Port 80 läuft&#8230; apache2! Trotz Deinstallation&#8230;

Na ja, ist eigentlich auch egal. Wichtig: Um den zu beenden einfach kill gefolgt von der PID (auf dem Screenshot rot markiert) ausführen. Also in meinem Beispiel:

`kill 3259`

In dem Sinne&#8230;

P.S.: Funktioniert mit Debian natürlich genauso.

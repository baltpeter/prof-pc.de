---
title: Proxmox (mit Console) hinter Nginx Reverse Proxy
author: Benjamin Altpeter
type: post
date: 2015-07-10T21:20:25+00:00
excerpt: Dieser Artikel erklärt, wie sich mit Nginx ein Reverse Proxy für die Proxmox-Weboberfläche einrichten lässt. Dieser funktioniert auch mit der noVNC Console.
url: /proxmox-console-nginx-reverse-proxy/
categories:
  - Allgemein
  - Tipps und Tricks
  - Tutorials
tags:
  - error 1006
  - nginx
  - novnc console
  - reverse proxy
  - ssl
  - websockets

---
Die Weboberfläche des <a href="https://www.proxmox.com/en/" target="_blank">Proxmox VE</a> läuft standardmäßig auf Port 8006 mit einem selbstsignierten SSL-Zertifikat. In diesem Artikel zeige ich, wie sich ein Reverse Proxy mit Nginx für das PVE-Webinterface einrichten lässt. Dies kann beispielsweise nützlich sein, um die Oberfläche über einen anderen Port (wie 443) abzurufen oder ein eigenes Zertfikat auszuliefern. Andere mögliche Anwendungszwecke wären das Einrichten eines Load Balancers oder das Verfügbarmachen des Web Interfaces außerhalb des eigenen Netzwerks (wobei hier natürlich besonders die Sicherheit im Auge behalten werden muss! Es empfiehlt sich zumindest das Einrichten von <a href="https://pve.proxmox.com/wiki/Two-Factor_Authentication" target="_blank">Two Factor Authentication</a>).

Grundsätzlich lässt sich dafür die übliche Konfiguration eines Nginx-Reverse Proxys verwenden (mit einer Ausnahme, s. unten):

<div class="gist-oembed" data-gist="baltpeter/3daf2469f972402b07ac.json">
</div>

Wichtig ist es hierbei natürlich, die folgenden Werte anzupassen:

  * `server_name`: Hier muss der FQDN eingetragen werden, auf den euer Reverse Proxy hören soll
  * `ssl_certificate`: Hier muss der Pfad zu eurem SSL-Zertifikat eingetragen werden
  * `ssl_certificate_key`: Hier muss der Pfad zum Private Key eures SSL-Zertifkats eingetragen werden
  * `proxy_pass`: Hier muss euer Proxmoxserver eingetragen werden (entweder über die IP oder den Hostname). Der Port 8006 muss erhalten bleiben.

Wie bereits erwähnt, handelt es sich bei dieser Konfiguration um die übliche, die man für einen Reverse Proxy mit Nginx verwenden würde. Unüblich sind lediglich die folgenden Zeilen:

```
# Enable websockets for the noVNC console to work
proxy_http_version 1.1;
proxy_set_header Connection $http_connection;
proxy_set_header Origin http://$host;
proxy_set_header Upgrade $http_upgrade;
```

Hierdurch werden die sogenannten Websockets aktiviert. Diese sind notwendig, damit die noVNC Console auch über euren Proxy funktioniert. Anderfalls würdet ihr beim Verbinden lediglich folgende Fehlermeldung erhalten: `Server disconnected (code: 1006)`.

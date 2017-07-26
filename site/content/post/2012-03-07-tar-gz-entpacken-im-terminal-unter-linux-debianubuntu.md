---
title: .tar.gz entpacken im Terminal unter Linux (Debian/Ubuntu)
author: Benjamin Altpeter
type: post
date: 2012-03-07T19:29:46+00:00
url: /tar-gz-entpacken-im-terminal-unter-linux-debianubuntu/
categories:
  - Allgemein
  - Text-/Bildtutorials
  - Tutorials
tags:
  - archiv
  - debian
  - entpacken
  - gz
  - konsole
  - linux
  - tar
  - terminal
  - ubuntu

---
Für die (wie mich), die auch ständig den Befehl zum entpacken von .tar.gz-Archiven vergessen:<!--more-->

>     tar xfvz [archivname].tar.gz

Und hier noch mal die Erklärung der Paramter:

<table>
  <tr>
    <td>
      -x
    </td>
    
    <td>
      steht einfach nur für &#8222;extract&#8220;, also entpacken
    </td>
  </tr>
  
  <tr>
    <td>
      -v
    </td>
    
    <td>
      steht für &#8222;verbose mode&#8220;, also die Dateien beim<br /> Entpacken anzeigen
    </td>
  </tr>
  
  <tr>
    <td>
      -f
    </td>
    
    <td>
      sagt dem Programm einfach nur, dass eine Datei<br /> angegeben wird, die entpackt werden soll
    </td>
  </tr>
  
  <tr>
    <td>
      -z
    </td>
    
    <td>
      sagt, dass das Archiv zunächst mit gzip entpackt<br /> werden soll
    </td>
  </tr>
</table>

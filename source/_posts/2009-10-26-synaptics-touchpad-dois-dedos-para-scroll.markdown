--- 
layout: post
title: Synaptics touchpad + dois dedos para scroll
wordpress_id: 152
wordpress_url: http://www.almirmendes.net/?p=152
date: 2009-10-26 16:52:57 -02:00
---
<span style="color: #ff0000;"><em><strong>Veja os comentários!</strong></em></span>

Amigos,

Essa é uma dica rápida. Estava eu vendo algumas matérias sobre SOs, e lá estava o MAC bonitão como sempre, vi então no vídeo um rapaz fazendo o scroll da tela (direcionando barra de rolagem) com dois dedos no touchpad do MAC, então pensei: Deve ter algo similar na configuração do Synaptics Touchpad que faça isso. E bingo!

Basta adiciona as diretivas abaixo junto a sua configuração do Synaptics no /etc/X11/xorg.conf:
<pre lang="xorg_conf">Section "InputDevice"
        ...
      Option      "VertTwoFingerScroll"   "true"   # vertical scroll anywhere with two fingers
      Option      "HorizTwoFingerScroll"  "true"   # horizontal scroll anywhere with two fingers
      Option      "EmulateTwoFingerMinZ"  "120"    # this may vary between different machines
        ...
EndSection</pre>
Adicionei apenas a primeira opção pois eu não gosto de scroll na horizontal, e também não precisei da emulação ativada com a terceira opção. Portanto faça o teste no seu notebook.

É isso amigos, vlw.

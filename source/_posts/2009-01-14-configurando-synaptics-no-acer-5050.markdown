--- 
layout: post
title: Configurando Synaptics no Acer 5050
wordpress_id: 39
wordpress_url: http://www.almirmendes.net/?p=39
date: 2009-01-14 13:40:09 -02:00
---
Olá amigos!

<img class="alignleft" title="Acer 5050" src="http://images.quebarato.com.br/photos/big/8/B/4FE8B_1.jpg" alt="Acer 5050-3284" width="225" height="225" />

Seguindo nossa saga de configuração do GNU/Linux para funcionar perfeitamente em um Acer Aspire 5050-3284, vamos agora configurar o toutchpad. Por padrão ele já funciona, mas não permite configurar um scrool (usando as bordas do touchpad) ou mesmo aquele direcional entre os dois botões.

Para configurar corretamente o touchpad você irá precisar do "<a title="Synaptics" href="http://web.telia.com/~u89404340/touchpad/" target="_blank">Synaptics touchpad driver for X.Org</a>". Se você utiliza alguma distribuição que possui esse software em seu repositório, proceda com a instalação conforme de costume, caso contrário proceda com o famoso trio: ./configure &amp;&amp; make &amp;&amp; make install.

Depois de instalado precisamos configurar o X.org. Vamos adicionar a seguinte entrada no arquivo xorg.conf:
<pre> Section "InputDevice"
 Identifier    "Synaptics Mouse"
 Driver        "synaptics"
 Option        "Device"                "/dev/psaux"
 Option        "Protocol"              "auto-dev"
# enable SHMConfig if you want to enable synclient
# NB: enabling SHMConfig is insecure, since any user can invoke it
#  Option        "SHMConfig"             "on"
 Option        "LeftEdge"              "1700"
 Option        "RightEdge"             "5300"
 Option        "TopEdge"               "1700"
 Option        "BottomEdge"            "4200"
 Option        "FingerLow"             "25"
 Option        "FingerHigh"            "30"
 Option        "MaxTapTime"            "180"
 Option        "MaxTapMove"            "220"
 Option        "VertScrollDelta"       "100"
 Option        "CornerCoasting"        "1"
 Option        "CoastingSpeed"         "3"
 Option        "MinSpeed"              "0.09"
 Option        "MaxSpeed"              "0.18"
 Option        "AccelFactor"           "0.0015"
#  Option       "Repeater"              "/dev/ps2mouse"
EndSection</pre>
Depois de adicionada essa entrada "InputDevice", procure agora pela seção: "ServerLayout", e adicione:
<pre>Section "ServerLayout"
...
InputDevice    "Synaptics Mouse" "SendCoreEvents"
...</pre>
Aqui vale relatar algo importante. No arquivo INSTALL que vem junto do fonte do Synaptics sugere que você adicione essa (código acima) entrada da seção ServerLayout com a opção "CorePointer", mas no meu Slackware 12.1 essa opção não funciona, fazendo com que o touchpad pare de funcionar também. Sendo assim, se na sua distro também não funcionar, utilize a opção "SendCoreEvents" conforme citado acima, e tudo vai dar certo. Salve o arquivo xorg.conf e saida dele.

Pronto, agora basta reiniciar o X e tudo deverá funcionar.

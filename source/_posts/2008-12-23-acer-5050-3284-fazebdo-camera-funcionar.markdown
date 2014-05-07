--- 
layout: post
title: "Acer 5050-3284 - Fazendo câmera funcionar no linux"
wordpress_id: 35
wordpress_url: http://www.almirmendes.net/?p=35
date: 2008-12-23 10:37:23 -02:00
---
A partir da versão 2.6.27 o kernel Linux passou a suportar nativamente o driver UVC - USB Video Class. Esse driver permite o suporte a inúmeras câmeras presentes na maioria dos notebooks e também dispositivos de câmera externos (USB).

Para ativar esse driver, baixe qualquer versão do kernel Linux a partir da série 2.6.27, e na configuração do kernel selecione a opção:
<pre>Device Drivers --&gt;
    Multimedia devices --&gt;
        Video capture adapters --&gt;
            V4L USB devices --&gt;
                &lt;M&gt; USB Video Class</pre>
Caso possua alguma câmera USB presente na listagem de dispositivos exibidos, aproveite para marcar também. Feito isso basta proceder com a compilação do kernel conforme o costume, e bom proveito.

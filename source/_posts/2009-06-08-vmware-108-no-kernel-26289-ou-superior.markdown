--- 
layout: post
title: VMware 1.0.8 no kernel 2.6.28.9 ou superior
wordpress_id: 101
wordpress_url: http://www.almirmendes.net/?p=101
date: 2009-06-08 14:53:42 -03:00
---
Olá amigos,

Esse post é rápido, o principal intuito é guardar uma dica que achei e pode ajudar a muitos.

A tempos o kernel 2.6.29 já saiu, e havia testado uma vez, mas tenho alguns recursos que ainda são amarrados no kernel 2.6.28, escpecialmetne o VMWare 1.0.8 (não gosto do 2).

Então aguardei por algum tempo até sair algum patch para o VMWare 1.0.8 rodar no novo kernel 2.6.29, eis que finalmente achei, e é isso que irei guardar aqui nesse post.

O que precisa ser feito é baixar o VMWare 1.0.8, se você ainda não o tiver, e depois baixar os sources compactados <a title="Fonte dos Módulos" href="http://www.almirmendes.net/downloads/vmware-server-modules-2.6.29.tar.gz">AQUI</a>.

Descompacte o arquivo vmware-server-modules-2.6.29.tar.gz dentro do diretório descompactado do VMWare 1.0.8:  ./vmware-server-redistrib/lib/modules/source/, depois proceda com a instalação.

Pronto.

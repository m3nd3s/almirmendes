--- 
layout: post
title: "IA-32 - Lembre-se caso v\xC3\xA1 compilar kernel Linux 64"
wordpress_id: 297
wordpress_url: http://www.almirmendes.net/?p=297
date: 2010-05-26 19:47:50 -03:00
---
Então,

Em uma das minhas últimas aventuras eu tive oportunidade de compilar meu primeiro kernel para um SO Linux 64bits, no caso era um openSuSE que insistia em não inicializar pelo RAID 1 que eu havia feito manualmente (sem usar o yast2). O processo de compilação é praticamente o mesmo.

Como dito acima, o motivo para compilar o kernel específico para a máquina foi a necessidade de adicionar o boot via RAID 1, já que mesmo criando o initrd para o SO padrão do openSuSE, com as opções de Raid e LVM, ele não inicializava por nada.

Como tratava-se de um openSuSE compilado para 64bits, assim que finalizei a compilação mandei ver no "reboot". O sistema inicializou normalmente, eu lá olhando e pensando: maravilha! maravilha, maravilhosidade completa!

Sistema carregado, é hora de continuar o processo de RAID, só que percebi que em algumas vezes (sempre) que eu chamava o yast2 uma mensagem de erro indicava problemas ao executar um tal ld-linux.so.2. Bem, pensei: "acho que não atualizou a lista de bibliotecas", então tome "ldconfig". Mas nada, continuou na mesma. Como não impedia o uso do yast2 eu deixei para depois.

Só que para continuar o RAID eu precisava gravar o grub também na MBR do segundo disco, e qual não foi minha surpresa quando o comando "grub" também não executava pois o mesmo erro acima citado voltava a aparecer! Então lá fui eu procurar o motivo e foi quando descobri que para ambientes Linux 64bits, se você vai querer habilitar compatibilidade com programas 32bits (e vc sempre precisa, o grub por exemplo é um binário 32bits) é necessário habilitar no kernel a opção IA32.

Essa opção fica na parte denominada <strong><em>"Executable files formats / Emulations"</em></strong> e só aparecerá se você estiver compilando um kernel para SOs 64 (lógico né! :)).

Então fica a dica: se for compilar kernel para SOs 64 não esqueça de marcar esta opção.

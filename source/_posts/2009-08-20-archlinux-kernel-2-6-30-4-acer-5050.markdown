--- 
layout: post
title: Archlinux + Kernel 2.6.30.4 + Acer 5050
wordpress_id: 128
wordpress_url: http://www.almirmendes.net/?p=128
date: 2009-08-20 19:47:03 -03:00
---
Olá amigos!

<img class="alignleft" title="Acer 5050" src="http://jualbeli.files.wordpress.com/2008/01/acer_aspire5051anwxmi.jpg" alt="" width="179" height="122" />Para não perder o costume vamos a mais novidades sobre o Acer 5050 no GNU/Linux. Vocês já devem saber que eu decidi instalar o Archlinux no meu notebook e deixar um pouco o Slackware de lado  - conforme cito no post anterior. O que poucos sabem é que eu mais uma vez esqueci de salvar meu .config do kernel e alguns outros conf que eu tinha.

Nesse caso eu tive que reconfigurar tudo do zero, e mais uma vez lá vai o m3nd3s meter as caras no kernel, e como alguns já sabem - <a href="http://www.almirmendes.net/2008/12/22/gnulinux-acer-5050-a-saga/" target="_self">leiam meus posts sobre o assunto</a> - o Acer 5050 vem com a DSDT/ACPI bugado.

Como eu estava enfrentando problemas ao compilar o novo kernel 2.6.30.4 no meu notebook, com a dsdt embutida, lembrei do blog de um colega de Notebook <a href="http://www.manifesto.blog.br/1.5/Projetos/Linux-no-Acer-5050/acer-5050-kernel-2630.html" target="_blank">Diogo Souza</a> - ele tem o mesmo notebook que eu e usa GNU/Linux, então fui visitá-lo (o blog) para saber se tinha alguma novidade. E não é que tinha!

Segundo o post dele, o kernel &gt;= 2.6.30 já vinha com suporte ao nosso hardware completamente, sem a necessidade de embutir a DSDT corrigida nele. E como eu estava tendo problemas ao compilar o kernel - o kernel congelava no boot - eu resolvi fazer a compilação sem incluir a DSDT nela, e bingo, kernel funcionando.

Bateria, controle de brilho, wireless, teclas especiais e tudo que tenho direito já funcionando, sem o sofrimento que eu enfrentava antes. Veja <a href="http://www.almirmendes.net/category/linux/" target="_self">AQUI</a>.

Então é isso amigos. Eu estou construindo um post sobre minhas experiências e ponto de vista sobre o Archlinux, então aguardem. (Só tenho que acabar a de PHP PDO antes.. rs)

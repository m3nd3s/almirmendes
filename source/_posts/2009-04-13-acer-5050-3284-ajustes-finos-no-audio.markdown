--- 
layout: post
title: Acer 5050-3284 - Ajustes finos no Audio
wordpress_id: 73
wordpress_url: http://www.almirmendes.net/?p=73
date: 2009-04-13 18:17:52 -03:00
---
Olá amigos!

Quem acompanha  meu blog, ultimamente meio desatualizado, percebe que tenho um Acer 5050-3289, e uso Slackware Linux.

Já tenho ele totalmente funcional, video, wireless, ACPI, Audio, etc... tudo! Mas hoje o meu gerente adicionou uma tarefa para a equipe técnica de nossa empresa, solicitando a configuração correta do audio do notebook de nossa gerente geral pois ela costuma utilizar o fone de ouvido para ouvir músicas, mas o notebook dela não estava "cortando" o som ao plugar o fone de ouvido, e isso gerava um desconforto a toda a equipe (não temos parede ou baias separando as equipes) e também a ela, que preferia ouvir sozinha...

Como no meu notebook aparecem dois controles para audio, tanto para as caixas externas quanto para o do plug do fone, nem esquentava com isso, até essa tarefa surgir. Daí comentei que no meu apareciam dois controles e meu gerente citou que havia a possibilidade de ativar esse recurso que permitiria o sistema desativar o audio das caixinhas e habilitar apenas a do fone.

Bem, com isso ele "ativou" meu modo de curiosidade e sai em busca, claro, principalmente para resolver o problema da gerente geral. E bingo, achei, para o meu caso e de todos os que tem o dispositivo (use o lspci para descobrir):

Audio device: ATI Technologies Inc IXP SB4x0 High Definition Audio Controller (rev 01)

Basta adicionar a seguinte linha no arquivo "/etc/modprobe.d/sound":
<pre>options snd-hda-intel model=acer-aspire</pre>
E pronto, daí você pode remover e recarregar o módulo usando os comandos como root:
<pre>modprobe -r snd_hda_intel</pre>
<pre>modprobe snd_hda_intel</pre>
Ou em casos mais drásticos, reiniciar o notebook.

Bem, é isso, na verdade estou postando para guardar o histórico, posso precisar disso outro dia. Agora vou ver no notebook da gerente.. rsrs

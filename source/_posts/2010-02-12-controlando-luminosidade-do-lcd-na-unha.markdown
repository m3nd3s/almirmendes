--- 
layout: post
title: Controlando luminosidade do LCD na "unha"
wordpress_id: 203
wordpress_url: http://www.almirmendes.net/?p=203
date: 2010-02-12 21:42:12 -02:00
---
Recentemente adquiri um<em> Dell Vostro 1320</em>, uma belezinha de máquina! Antes desta aquisição eu utilizava um Acer 5050 como notebook pessoal, diga-se  de passagem  que ele me rendeu boas dores de cabeça, muitas compilações de kernel e sobreposição da DSDT - <em>differentiated system description table</em> - até o advento do kernel 2.6.30.

Mas o notebook da Acer possui algumas teclas de função especial que controlam o brilho do LCD, em especial uma que desligava o LCD, tecla que esse meu novo Dell não possui.

<img class="alignleft" style="margin-left: 5px; margin-right: 5px;" title="Turn Off" src="http://www.geekpedia.com/Pictures/Icons/leopard-glass-power-off-button_128x128.png" alt="" width="128" height="128" />Essa tecla me fazia muita falta, especialmente quando eu utilizava o notebook longe de alguma tomada, o que me forçava a utilizar sua bateria, e nessas horas qualquer economia relacionada a carga da bateria é bem vinda, e nada melhor que desligar o LCD nos momentos de "ócio" do notebook, mas eu não tinha como desligar o LCD por falta dessa tecla especial.

Então pensei: <em>"Eu uso Linux! Deve ter um comando que controla isso!". <span style="font-style: normal;">Iniciei </span></em>minhas pesquisas na internet e depois de alguns cliques cheguei ao <a title="LessWatts" href="http://www.lesswatts.org" target="_blank">LessWatts</a> e também a alguns outros sites que contemplavam o assunto. Minha pesquisa não só me permitiu descobrir o comando que liga/desliga o LCD como também os comandos para aumentar ou diminuir o brilho do LCD. Segue abaixo:

Para desligar o LCD use <em>(Qualquer movimento de mouse ou tecla reativará o LCD)</em>:
[cc lang="bash"]xset dpms force off[/cc]
Para decrementar o brilho do LCD:
[cc lang="bash"]xbacklight -dec 20[/cc]
Para incrementar o brilho do LCD:
[cc lang="bash"]xbacklight -inc 20[/cc]
Os números informados para o comando <strong>xbacklight</strong> estão em porcentagem. Além da opção <em>-dec</em> e <em>-inc</em> há também o <em>-set</em> que define exatamente o valor passado - também em porcentagem.

Para obter o valor atual de brilho
[cc lang="bash"]xbacklight -get[/cc]
Agora basta definir teclas de atalho para cada um, isso se o seu gerenciador gráfico ainda não o fez, e ser feliz.

Um<em> man xse</em>t e <em>man xbacklight</em> é sempre bom! Uma visita ao link do<a title="LessWatts" href="http://www.lesswatts.org" target="_blank">LessWatts</a> pode lhe ajudar a não só economizar bateria com o ajustes no  LCD mas também em outros periféricos do seu notebook, vale a visita.

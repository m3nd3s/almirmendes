--- 
layout: post
title: "Meu Projeto de Conclusão de Curso, usando Arduino"
wordpress_id: 609
wordpress_url: http://www.almirmendes.com/?p=609
date: 2011-12-05 18:12:38 -02:00
---
# A ideia
Finalmente finalizei meu Trabalho de Conclusão de Curso (TCC), defendi/apresentei no dia 16 de novembro na <a href="http://site.faesa.br">FAESA</a>, faculdade em que estou cursando graduação em Ciência da Computação.

O trabalho foi feito em parceria meu grande amigo Renato Tecchio. O título dado ao nosso trabalho foi <strong>"Aplicação embarcada para monitoramento de temperatura em câmaras climatizadas"</strong>. O objetivo principal do trabalho era implementar um sistema embarcado para medir, registrar e monitorar câmaras climatizadas.

Baseado nas exigências da Agência Nacional de Vigilância Sanitária (ANVISA), mais especificamente nas portarias que regem o controle de temperatura de câmaras para armazenamento de alimentos, a nossa missão era, em resumo, implementar um sistema embarcado que pudesse medir e registrar as temperaturas câmaras climatizadas, e além disso que o sistema pudesse informar e notificar ao responsável quando a temperatura estivesse fora dos níveis aceitáveis.

Ao final o trabalho foi implementado em dois sistemas, um módulo registrador (usando Arduino) e um outro sistema (chamamos de Servidor de Dados e Monitoramento), implementado em Ruby on Rails, que era responsável por consumir os dados registrados pelo(s) Arduino(s) e com isso fornecer relatórios e gráficos. Também era responsabilidade do Servido de Dados e Monitoramento notificar, via SMS e/ou e-mail, o usuário sobre qualquer discrepância detectada entre as capturas de temperatura (realizadas pelo Módulo Registrador).

Ambos os sistemas foram implementados com interface web. Agora imagina o trabalho para implementar um simples formulário HTML que enviasse os dados via POST e posteriormente gravasse os dados em um arquivo. Pois é, nós fizemos isso :).

<img class="size-medium wp-image-615" title="Foto do protótipo - Módulo Registrador (Arduino)" src="http://www.almirmendes.com/wp-content/uploads/2011/12/Foto_prototipo2-300x295.jpg" alt="Protótipo" width="300" height="295" /></a>[/caption]
<h4>O começo</h4>
Inicialmente pensamos em implementar tanto o hardware quanto o software, mas vimos que isso nos tomaria muito tempo, mais do que o que poderíamos dispor no momento.

Começamos então uma procura de um hardware que atendesse ao nosso projeto. O nosso orientador, o professor Marcelo Brunoro, indicou alguns hardwares existentes no mercado, mas o preço nos assustou um pouco. Partimos então para o "Saint Google" em busca de algum hardware que nos atendesse.

Entretanto, foi em uma conversa com outro amigo, outro Renato, o <a href="http://renatocunha.com/about/">Renato Cunha</a> que me fez a indicação do Arduino, e foi como que paixão a primeira vista. Fiquei impressionado com a <a href="http://www.arduino.cc/playground/Projects/ArduinoUsers">quantidade de projetos</a> já implementados com Arduino e a capacidade dessa plaquinha, não tive dúvidas e compartilhei a descoberta com o Renato Tecchio que também aprovou. Decidimos então então utilizar o Arduino em nosso projeto.

[caption id="attachment_618" align="aligncenter" width="300" caption="Arduino Duemilanove"]<a href="http://www.almirmendes.com/2011/12/05/meu-projeto-de-conclusao-de-curso-usando-arduino/arduinoduemilanove/" rel="attachment wp-att-618"><img class="size-medium wp-image-618" title="Arduino Duemilanove" src="http://www.almirmendes.com/wp-content/uploads/2011/12/ArduinoDuemilanove-300x187.png" alt="Arduino Duemilanove" width="300" height="187" /></a>[/caption]

Pesquisamos por quem revendia o Arduino aqui no Brasil, localizamos um revendedor e compramos as placas Arduino e Ethernet shields. Depois disso compramos um monte de "quinquilharias" para plugar ao Arduino, diga-se de passagem a maioria dessas "quinquilharias" foram adquiridas no <a href="http://www.soldafria.com.br/">Solda Fria</a>, que eu recomendo.
<h4>Mãos a obra</h4>
<em>Comentar sobre a parte de documentação (referências) é um pouco chato, caso tenha interesse em saber quais foram as referências que usamos para o trabalho peço que entre em contato, vou comentar aqui sobre o que utilizamos para o trabalho.</em>

Utilizamos para nosso trabalho basicamente 4 componentes/dispositivos:
<ul>
	<li>A placa <a href="http://arduino.cc/en/Main/arduinoBoardDuemilanove">Arduino Duemilanove</a></li>
	<li>O sensor de temperatura <a href="http://www.maxim-ic.com/datasheet/index.mvp/id/2815">DS18S20</a></li>
	<li>O relógio de tempo real <a href="http://www.maxim-ic.com/datasheet/index.mvp/id/2685">DS1302</a></li>
	<li>Uma <a href="http://www.arduino.cc/en/Main/ArduinoEthernetShield">ethernet shield</a></li>
</ul>
[caption id="attachment_623" align="alignleft" width="150" caption="Sensor de Temperatura DS18S20. FONTE: http://martybugs.net"]<a href="http://www.almirmendes.com/2011/12/05/meu-projeto-de-conclusao-de-curso-usando-arduino/img_10288_600/" rel="attachment wp-att-623"><img class="size-thumbnail wp-image-623" title="Sensor de Temperatura DS18S20" src="http://www.almirmendes.com/wp-content/uploads/2011/12/IMG_10288_600-150x150.jpg" alt="Sensor de Temperatura DS18S20" width="150" height="150" /></a>[/caption]

Na época em que compramos nossas placas Arduino ainda não tinham chegado aqui ao Brasil a Arduino Uno, que era versão mais nova das placas do Projeto Arduino.

Obviamente precisávamos de um sensor de temperatura, afinal o objetivo do nosso trabalho dependia da leitura de temperaturas. A escolha do sensor DS18S20 foi simplesmente pela facilidade de já existirem drivers/bibliotecas para sua utilização com o Arduino.

Por fim o DS1302, um relógio de tempo real (Real Time Clock - RTC). Talvez você não saiba, mas o Arduino não possui um relógio. Em nosso trabalho nós precisávamos de, além de registrar a temperatura, registrar junto a temperatura o momento em que a leitura foi realizada, por isso o uso de um RTC no projeto. A escolha do modelo DS1302 também foi por já existirem bibliotecas prontas para a comunicação do dispositivo com o Arduino.

Depois de tudo adquirido foi só juntar tudo e programar, e foi aí que o bicho pegou!
<h4>Aprendizado</h4>
Sem sombra de dúvidas foi uma experiência muito proveitosa!

Entendemos, por experiência própria, o que significa a expressão "Enxugar bits". A Arduino Duemilanove possui 32K de memória flash, dos quais 30K são utilizada para armazenar o sistema embarcado. Possui também 2K de memória SDRAM, esta por sua vez é utilizada para rodar o programa embarcado.

[caption id="attachment_621" align="alignright" width="150" caption="DS1302 e o Cristal"]<a href="http://www.almirmendes.com/2011/12/05/meu-projeto-de-conclusao-de-curso-usando-arduino/17810-img_3251_pl/" rel="attachment wp-att-621"><img class="size-thumbnail wp-image-621" title="DS1302 e o Cristal" src="http://www.almirmendes.com/wp-content/uploads/2011/12/17810-img_3251_pl-150x150.jpg" alt="DS1302 e o Cristal" width="150" height="150" /></a>[/caption]

Como puderam perceber o nosso projeto considerava o uso do RTC e o sensor de temperatura, isso implica em carregar as bibliotecas de cada um desses dispositivos. Além disso trabalho contemplava a implementação de um sistema web que permitisse ao usuário configurar o próprio dispositivo (descrição, temperaturas críticas, endereço mac, endereço IP, máscara, relógio, etc). Tudo isso e ainda todo processamento backend.

Resumindo, tivemos que enxugar muitas partes de nosso código para que isso tudo coubesse dentro de 30K, foi uma tarefa difícil, mas que conseguimos vencer.

Outra coisa aprendida é que saber C++ ajuda muito. O Projeto Arduino usa como linguagem para desenvolvimento dos sketchs (nome dado aos programas criados para arduino) uma linguagem <strong>baseada</strong> em C++. Nem eu e nem o Renato tínhamos conhecimentos sobre a linguagem C++, nós fomos aprendendo enquanto o trabalho se desenrolava.

Vimos também o poder dessa plaquinha. O Projeto Arduino tem o objetivo de fornecer uma placa de prototipagem, que pudemos comprovar, sem sombra de dúvidas, que cumpre com louvor seu objetivo de prototipar sistemas. Antes mesmo de terminar o nosso trabalho eu já estava com uma lista de projetos para <em>brincar</em> quando terminasse, e é exatamente o que farei daqui para frente.
<h4>E agora?</h4>
Agora é só diversão. Como comentei acima eu tenho uma lista de projetos para brincar, alguns muito simples, outros mais audaciosos (que pretendo fazer em parceria com o mano @tagliati e @amenderdesign). Para essa troca de experiências nós (@tagliati, @amendesdesign e eu) criamos uma lista para discussão, chamada <a href="http://groups.google.com/group/openmadlab">OpenMadLab</a>, onde algumas pessoas já estão trocando ideias. Já estamos inclusive gerindo para 2012 um evento, que está agarrado desde o início do ano devido minha ocupação com o TCC, mas agora com o seu término nada nos impede.

Ainda publicarei uma série de outros artigos sobre Arduino, contando com detalhes (e códigos) o que pude aprender nesse 1 ano de TCC/Arduino.

Esse post foi apenas para dar um ponto de partida em uma série e posts sobre Arduino e conta um pouco minha experiência com essa plaquinha, por isso não tem código ou coisas do tipo, mas o próximo com certeza terá. Estou pensando em partir de algo básico e com o tempo vamos incrementando e aumentando as funcionalidades ;).

Obrigado e até mais.

--- 
layout: post
title: GNU/Linux + Acer 5050 - A Saga!
excerpt: "Devido uma incompatibilidade entre estes notebooks Acer 5050 e o kernel Linux, o ACPI, e consequentemente alguns outros dispositivos, n\xC3\xA3o configuram corretamente. Este problema provavelmente \xC3\xA9 proveniente de falta de padroniza\xC3\xA7\xC3\xA3o dos desenvolvedores do software Phoenix BIOS. Esse \xC3\xA9 o motivo de tanta dor de cabe\xC3\xA7a nesses notebooks.\r\n\
  \r\n\
  Devido a esse problema, o notebook n\xC3\xA3o desliga sozinho ao digitar o comando shutdown ou mesmo o halt. Aliado a isto, alguns outros itens podem simplesmente n\xC3\xA3o funcionar enquanto n\xC3\xA3o corridigo esse problema.\r\n\
  \r\n\
  Para resolver esse \"pepino\", precisaremos recompilar o kernel, ent\xC3\xA3o vamos a obra."
wordpress_id: 30
wordpress_url: http://www.almirmendes.net/?p=30
date: 2008-12-22 16:55:42 -02:00
---
Olá amigos, finalmente resolvi postar algo útil em meu blog depois de tanto tempo. Estive pensando em postar esse conteúdo todo em um único Post, mas achei que poderia ficar muito massante e possívelmente ficaria "chato" de achar algum conteúdo específico em um Post tão grade, pois então resolvi postar em partes diferentes, cada uma com um "capítulo" diferente.

Como este é o primeiro artigo, quero informar que o motivo que tenho para postar tal conteúdo é, antes de mais nada, para que eu  tenha guardado em algum lugar o que fiz para configurar em meu Slackware (na data do post a versão era 12.1)  o notebook da Acer, modelo 5050, mais específicamente o Acer Aspire 5050-3284.

[caption id="" align="alignleft" width="132" caption="Acer 5050-3284"]<img title="Acer 5050-3289" src="http://www.eatec.com.br/fotos/notebooks/5050_p.jpg" alt="" width="132" height="104" />[/caption]

Vamos começar pelo básico, mas porém o mais complicado. Devido uma incompatibilidade entre alguns destes notebooks Acer 5050 e o kernel Linux, o ACPI, e consequentemente os dispositivos que dependem do ACPI, não configuram corretamente. Este problema provavelmente é proveniente de falta de padronização dos desenvolvedores do software Phoenix BIOS utilizado nesses notebooks. Esse é o motivo de tanta dor de cabeça para por o GNU/Linux funcionando diritinho, e olha que esses notebooks já vem com GNU/Linux instalado.

Devido a esse inconveniente, o notebook não desliga sozinho ao digitar o comando <strong>shutdown</strong> ou mesmo o <strong>halt</strong>, e sequer mostra o status da bateria. Aliado a isto, alguns outros itens podem simplesmente não funcionar enquanto não corrigido esse problema.

Para resolver esse "pepino", precisaremos recompilar o kernel, então vamos a obra.

Não irei abordar uma compilação de kernel aqui, não é o foco, e também não sou expert nisso. Se você ainda não sabe como fazer isso, dê uma breve pesquisada na internet sobre o assunto, vale a pena! Uma boa idéia é pegar o <strong><em>.config</em></strong> de seu kernel atual e usá-lo como base, apenas tenha atenção de marcar como buildin (imbutido no kernel "*") o sistema de arquivos e o driver da controladora do seu HD, caso contrário serás presenteado com um Kernel Panic.

Bem, de qualquer forma precisaremos da DSDT - Differentiated System Description Table -  para nosso Acer 5050. Existem duas formas de se obter essa DSDT:
<ul>
	<li>Você mesmo desassemblar ela, corrigir os erros, e utilizá-la.</li>
	<li>Obter alguma na internet</li>
</ul>
Caso vá utilizar a primeira, procure na internet como corrigir os erros, eu sugiro pesquisar exatamente pelo seu modelo, para evitar problemas ainda maiores. Ao final da página eu cito um link para começar a busca.

Caso vá utilizar a segunda, abordada aqui nesse Post, tenha apenas a certeza de estar utilizando a DSDT correta para  seu modelo. Eu utilizo um Acer 5050-3284, e estou disponibilizando <a href="http://www.almirmendes.net/downloads/dsdt.hex" target="_self">AQUI a DSDT que utilizei para ele</a>.

Beixe a DSDT, salve-a no diretório /usr/src. Agora vamos editar o .config de seu kernel adicionando/alterando os seguintes atributos:
<pre class="command">CONFIG_STANDALONE=n
CONFIG_ACPI_CUSTOM_DSDT=y
CONFIG_ACPI_CUSTOM_DSDT_FILE="/usr/src/dsdt.hex" #Cuidado com o Case-sensitive</pre>
Feito isto, agora proceda com a compilação do seu kernel conforme está acostumado a fazer, instale o kernel, reinicie o notebook e pronto!

Alguns links úteis:
<ul>
	<li><a href="http://www.dicas-l.com.br/dicas-l/20040710.php" target="_blank">Recompilando o kernel</a></li>
	<li><a href="http://www.lesswatts.org/projects/acpi/overridingDSDT.php" target="_blank">Sobrescrevendo uma DSDT</a></li>
	<li><a href="http://www.kernel.org" target="_blank">Kernel Linux</a></li>
	<li><a href="http://www.lesswatts.org/projects/acpi/index.php" target="_blank">Linux ACPI</a></li>
</ul>

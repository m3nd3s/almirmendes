--- 
layout: post
title: PKGBUILD do AdvanceMAME
wordpress_id: 181
wordpress_url: http://www.almirmendes.net/?p=181
date: 2010-01-24 14:29:48 -02:00
---
Me considero um amante de jogos modelo arcade, ou para os mais "íntimos": fliperama. Quando eu era apenas um moleque vivia gastando os poucos centavos que conseguia "arrumar" para jogar fliperama.

<img class="alignright" title="Arcade" src="http://www.tradeboothtrafficbuilder.com/images/arcade_game.jpg" alt="" width="300" height="300" />Ainda me lembro da primeira vez que vi um arcade. Eu retornava da escola para casa, onde na época eu cursava o que hoje é chamado de nível fundamental, nesse caminho passei em frente a uma dessas casas de jogos, havia várias máquinas - como costumavamos chamar os arcades - uma ao lado da outra. Dentre elas havia uma com um joguinho que tinha um cavaleiro lutando contra monstros, fantasmas, animais bizarros, etc.

Essa foi a época do boom desses jogos arcade, foi justamente quando a Capcom lançou Street Fighter II. As casas de jogos viviam cheias de "competidores".

Havia uma plaquinha pregada na parede da casa de jogos, num local que podia ser visto por qualquer pessoa que se aproximasse da entrada, a placa dizia<em> "Não é permitida a permanência de estudantes"</em>, então fui em casa para trocar de roupa. E criança é criança né! Não pensa que roupa vai usar, apenas pega a primeira que vê pela frente e usa. Fiz exatamente isso e retornei mais tarde para jogar.

Entretanto fui surpreendido com uma calorosa frase de boas vindas:<em> "Aqui você não pode entrar!"</em>. E o rapaz que me dizia essa frase apontou para a minha camisa. Bem, qual não foi minha surpresa quando vi que troquei a camisa da escola por uma outra camisa de escola, porém da escola que eu frequentei até a 2º série - nessa época eu deveria estar na 3ª ou 4ª série.

Triste e morrendo de vontade de jogar retornei para minha casa, e no caminho  havia um barzinho com uma dessas máquina de fliperama (arcade). Não era a mesma, porém eu estava com muita vontade de jogar. O jogo era o de um "carro" que andava sobre um terreno irregular e atirava em outros objetos acima e à frente do carro.

Comprei minha ficha e desde então começou minha paixão/vício, que só foi parar quando começei a trabalhar e ver o quanto custa ganhar dinheiro. :-D

Há poucos anos descobri que eu poderia jogar esses jogos no computador, através do que conhecemos como emulador. Fazendo pesquisas  na internet descobri o MAME, na época versão para o MS Windows. E quando começei a usar GNU/Linux procurei algo equivalente, e encontrei o AdvanceMAME.

<a href="http://advancemame.sourceforge.net"><img class="aligncenter" title="AdvanceMAME" src="http://advancemame.sourceforge.net/mame-logo.png" alt="" width="598" height="71" /></a>

O AdvanceMAME é um emulador, não oficial, de MAME. A página do projeto pode ser visitada <a href="http://advancemame.sourceforge.net" target="_blank">AQUI</a>.

O que disponibilizo para vocês é o <a title="PKGBUILD" href="http://www.almirmendes.net/downloads/advancemame.tar.gz" target="_blank">PKGBUILD</a> para distribuições Arch Linux, ainda não me senti a vontade para postar ele no AUR. Caso encontre algum bug, por favor reporte, ficarei feliz em corrigir. Se você utiliza Slackware, baixe o <a href="http://slackbuilds.org/repository/13.0/games/advancemame/" target="_blank">SlackBuild</a>, a propósito agradeço o 'seb' (Sebastien) que criou o slackbuild,  já que usei-o como base para criar o PKGBUILD.

Para instalar, baixe o PKGBUILD no link acima, descompacte, entre no diretório criado e rode o comando makepkg, tudo como usuário normal. O pacote será gerado, agora instale-o como root com o comando:
<pre lang="bash">pacman -U nome-do-pacote-gerado.pkg.tar.gz.</pre>
O binário <strong>advmame</strong> será salvo em /usr/games. Adicione esse path no /etc/profile na variável PATH.

A forma certa de chamar o emulador é:
[cc lang="bash"]advmame nomerom[/cc]
Se você reparou bem, não tem a extensão e nem o path. É necessário que você altere a configuração do AdvanceMAME para apontar o path onde estão os ROMs.

Para configurá-lo execute o comando <strong>advmame</strong> sem parâmetros, ele criará o arquivo de configuração e lhe dirá qual o path default dos roms e como alterá-lo.

Sobre os joguinhos que comentei no início do post, caso tenha ficado curioso, eles são:
<h3>Ghosts'n Globins</h3>
<p style="text-align: center;"><img class="aligncenter" title="Ghosts'n Globins" src="http://upload.wikimedia.org/wikipedia/en/7/73/Gngarcade.png" alt="" width="256" height="224" /></p>

<h3>Moon Patrol</h3>
<p style="text-align: center;"><img class="aligncenter" title="Moon Patrol" src="http://www.gameclassification.com/files/games/moon_patrol.gif" alt="" width="240" height="248" /></p>
Hoje já parti para outros inúmeros títulos mais "recentes" como: Street Fighter, The King of Fighters, Fatal Fury, Bomberman, Black Tiger, Capitão Comando, Dungeons dragons e muitos outros, todos emulados.

O melhor site para baixar ROMs  na minha opinião, é o <a title="Roms World" href="http://www.rom-world.com/ " target="_blank">Roms World</a>. ROMs são os jogos empacotados em formato zip, os quais você usa para carregar no emulador e jogar.

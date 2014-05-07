--- 
layout: post
title: "Archlinux - Primeiras impressões"
wordpress_id: 145
wordpress_url: http://www.almirmendes.net/?p=145
date: 2009-09-07 15:41:30 -03:00
---
Pois bem senhores, conforme havia prometido vou lhes descrever como está a minha utilização do Archlinux e o que eu "vejo" nesta distro.

Antes de começar, para aqueles que não me conhecem, eu sou usuário do Slacware. Sim, ainda me considero um Slacker e portanto o meu ponto de vista sobre o Archlinux pode sofrer algumas influências e comparações com essa distro.

Imagino que uma pergunta pertinente nesse post seria: <em><strong>"Porque você deixou de usar Slackware e passou a usar o Archlinux?"</strong></em>.

Primeiro acho que deixar de usar Slackaware seria uma expressão um tanto forte demais, eu diria que resolvi testar o Archlinux. Como falei, sou Slacker, e como bom Slacker eu gosto de aprender bastante sobre um sistema Linux. Usar uma distro que <em>"fizesse tudo por mim"</em> não é o que eu quero. Já utilizo Slackware há mais de 5 anos: simplicidade, exigência de conhecimento sobre o ambiente, poucas ferramentas<em> "user friendly"</em> para <em>"ajudar"</em> na configuração do sistema, grupos de usuários com bons conhecimentos, etc.

Um certo dia um amigo, <span style="text-decoration: underline;">Janderson</span>, me mandou um e-mail com um link, onde um rapaz falava muito bem do Archlinux, sobre sua simplicidade, sua filosofia, um gerenciador de pacotes bom, dentre outras coisas, gostei muito do que li e fiquei com uma vontade de testar essa distro.

Mas antes do <span style="text-decoration: underline;">Janderson</span> me enviar o e-mail, eu havia tido uma experiência um tanto<em> "traumática"</em> em um cliente da empresa que trabalho. Fomos solicitados para atender a um cliente com problemas em seu servidor de e-mails, resumindo a história, chegamos lá e demos de cara com um Gentoo Linux, como eu nunca havia manuseado um Gentoo Linux, demorava para saber onde estavam alguns itens. Minha experiência se limitava às distros como: Slackware(s), Debian(s) e RPMs distros (RedHat, Fedora, CentOS, SuSE...). E se existe algo que me deixa muito <em>"grilado"</em> é quando eu preciso fazer algo mas não sei <em>"o que e onde estão e como faço tal coisa aqui?"</em>. Desde esse dia, então, eu decidi testar outros sabores de Linux para não mais passar por essa situação.

Desde esse dia começei a pesquisar por outras distros e suas filosofias, inclusive fiz uma palestra no <a href="http://www.almirmendes.net/2009/04/27/flisol-2009/" target="_self">FLISOL 2009</a>, aqui em Vitória/ES, sobre o assunto. E dentre elas me simpatizei com o <strong>Gentoo Linux</strong> e o <strong>Archlinux</strong>.

<img class="alignleft" src="http://upload.wikimedia.org/wikipedia/commons/thumb/1/1e/Archlinux-icon-128.svg/128px-Archlinux-icon-128.svg.png" alt="" width="128" height="128" />Então eu já tinha as distros que eu queria testar, mas precisava decidir qual delas seria a primeira, e a escolhida foi Archlinux! O motivo? Simples, eu demoraria mais tempo instalando e configurando o Gentoo do que o Archlinux.

Então fiz a instalação, fiz um backup das minhas coisas no notebook para o PC da minha esposa, coloquei o CD de instalação e mandei ver!

Eu praticamente não tive problema algum com a instalação do Archlinux, por dois motivos principais: <strong>1</strong> - Eu sou Slacker! e <strong>2 </strong>- A documentação do Archlinux é simplesmente fantástica. Você acha praticamente tudo que precisa no wiki oficial - <a href="http://wiki.archlinux.org" target="_blank">http://wiki.archlinux.org</a> - e também na versão mantida por nossos amigos basucas - <a href="http://wiki.archlinux-br.org/" target="_blank">http://wiki.archlinux-br.org/</a>.

Então finalmente finalizada a instalação básica, você tem um sistema básico. E é a partir daqui que faço minhas observações. O Archlinux tem uma filosofia semelhante (eu diria igual) à do Slackware: <em>KISS</em>! Essa filosofia guia a distro para a construção de um sistema simples, mas simples não do ponto de vista de facilidade, moleza, mas de quanto menos ferramentas para atrapalhar o usuário, melhor!

Não espere dos desenvolvedores do Archlinux interfaces GUIs que auxiliem ao usuário na administração do sistema, mas sim ferramentas que permitam o usuário a fazer exatamente o que ele quer. Então para quem usa o Slackware, está mais que ótimo!

Outra observação sobre o Archlinux é que diferente da maioria das distribuições existentes, o Archlinux não instala um sistema <em>"completo"</em> logo no início a partir do CD, na verdade o que você tem é um sistema básico, mas básico mesmo, e utilizável para dar continuidade no processo de instalação e ir instalando os pacotes que você necessita. A instalação básica permite que você se conecte à internet, ou a uma rede, para a partir dalí instalar o que você quer. Esse é outro ponto interessante da distro e que pode afastar algumas pessoas interessadas: Se você não tem um link de internet bom, fica praticamente inviável usar o Archlinux. Isso porque, como citei acima, o que é instalado pelo CD de instalação, é um sistema BÁSICO! Você deve instalar o restante dos pacotes que deseja a partir dos mirros da distro. (e eu dei meu jeitinho)

<img class="alignright" src="http://www.wired.com/images_blogs/photos/uncategorized/2007/06/04/pacman_2.gif" alt="" width="147" height="142" />A partir desse ponto iniciasse a etapa de instalação dos pacotes, e mais um item que me chamou a atenção no Archlinux, o gerenciador de pacotes pacman. Esse poderoso software é o responsável por quase TUDO que você precisa em termos de instalação de pacotes. O pacman instala pacotes e resolve dependências assim como o apt faz no Debian. Não farei aqui uma comparação entre o apt e o pacman, acho que isso não vai levar à lugar algum.

O repositório do Archlinux é constantemente atualizado, e quando digo constante é constante mesmo! O Arch, como é chamado pelos mais íntimos, não trabalha com releases, versões. Por isso não se ouve falar da versão X ou Y do Archlinux. Os CDs são apenas o sistema básico preparado de tempos em tempos para permitir uma instalação e a partir dela fazer todo o resto, especialmene a atualização da distro. Uma vez instalado o sistema, para se atualizar tudo você roda apenas um comando: <strong>pacman -Syu</strong>.

Como já havia comentado, tudo que você precisa saber sobre como lidar com o Archlinux está disponível nos wikis oficiais, e é visita obrigatória caso deseje usar o Archlinux. Lá você encontra desde itens pertinentes apenas a própria distro enquanto sistema, quanto também sobre configuração de hardware, instalação de softwares específicos, drivers, etc. É um show a parte a documentação do Archlinux.

Os arquivos de configuração do Arch são tão simples como os do Slackware, arquivos textos disponíveis em /etc e também possui em cada um deles os devidos comentários sobre as sessões/parâmetros disponíveis.

O Arch é compilado e otimizado para rodar em arquiteturas i686, isso o deixa mais rápido, especialmente se comparado ao Slackware já que este último compila seus pacotes par arquitetura i486. Temos então uma vantagem e <em>"desvantagem"</em>. A vantagem é um sistema mais rápido, e isso eu pude perceber de cara, graças a otimização para i686. E a <em>"desvantagem" </em>(com aspas mesmo) é pelo fato do Arch nunca poder ser instalado em um PC antigo, mas pense um pouco: O que é um hardware antigo hoje em dia? Eu já estou achando os PIII antigos.. rs.

E chegando ao final do meu post, quero aproveitar para elogiar aos desenvolvedores e a comunidade de Archers pela ótima e farta documentação sobre a distro, até o momento não fiquei na mão em nada que eu precisasse descobrir. Parabéns a todos.

Por enquanto é isso amigos, do mais vejo o Archlinux como qualquer outro Linux. Mas se você pretende tirar LPI um dia, minha sugestão de distros para esse fim são Debian Linux e o saudoso Slackware. Você pode instalá-los em uma VM, usando VMWare ou KVM Linux.

---
layout: post
title: "Meu ambiente de trabalho em 7 itens: 2013"
date: 2013-05-13 14:19
comments: true
categories: environment [environment, seven, items, workspace, work, developer]
---

Em 20 de janeiro de 2011, inspirado por um post da Loiane, eu publiquei um post sobre as ferramentas que utilizo em meu ambiente de trabalho. Com o passar do tempo é comum que façamos mudanças em nosso ambiente visando melhorar e agilizar nosso processo de trabalho. Então resolvi dar uma atualizada no post para mostrar como e o que estou usando agora.

## 1. Navegador

Como desenvolvedor web o navegador é uma ferramenta essencial. Há muitos anos vinha utilizando o [Mozilla Firefox](http://www.mozilla.org/en-US/firefox/new/) mas de uns tempos pra cá ele vinha me decepcionando.

Ao menos em minha máquina o Firefox comia muita memória e não raro travava enquanto abria determinada página. Outro problema eram as extensões que eu precisava instalar para torna-lo uma ferramenta de trabalho (Firebug, WebDeveloper, etc).

Hoje abro os demais navegadores apenas para fazer testes nos sistemas que trabalho. É impressionante as informações que podemos extrair através do Developer Tools do Google Chrome, até hoje não aprendi todas. Abaixo deixo alguns links que julgo ser imprecindíveis para quem desenvolve aplicações web, mais específicamente para quem tem o Google Chrome como opção:

* [Chrome DevTools](https://developers.google.com/chrome-developer-tools/)
* [Code School Discover DevTools](http://discover-devtools.codeschool.com/)

## 2. Editor

Neste caso não há uma mudança grande ou significativa, sempre utilizei Vim como editor principal e já estou tão acostumado que me minha produtividade em outro editor chega a ser péssima.

Assim que comecei a usar o sistema MacOS eu conheci o [MacVim](https://github.com/b4winckler/macvim), instalei e desde então o utilizava. Um dos motivos que me fazia utiliza-lo era, principalmente, que um dos plugins que eu utilizo, o [CommandT](https://wincent.com/products/command-t), dependia do Vim com suporte a ruby. Como o vim padrão do MacOS não possuía suporte e eu não tinha vontade de compilar o na unha, eu utilizava o MacVim.

Com o uso do [homebrew](http://mxcl.github.io/homebrew/) descobri que o Vim dele incluía suporte a ruby, isso e a vontade de usar o Tmux (leia abaixo) me fizeram largar do MacVim  para o vim.

## 3. Tmux

Talvez a mudança/melhoria mais significativa. Ao menos uma coisa é certa, mantenho minha mente e memória ocupados por um bom tempo tendo que decorar mais algumas teclas de atalho, mas nem tanto.

O [Tmux](http://tmux.sourceforge.net/) é um terminal multiplexer, basicamente é um programa que lhe permite manipular vários programas em um único terminal, assim como o velho conhecido de usuários Unix Like, o [GNU screen](http://www.gnu.org/software/screen/). A diferença é que o Tmux tem várias features que o transformam em uma opção considerável para programadores que utilizam editores em modo texto. Recomendo olhar na internet alguns vídeos de integração Tmux + Vim + Ruby.

Meu interesse nele surgiu pela vontade de reduzir ainda mais o uso de cliques para escolher janelas e navegar entre elas e as features que ele possui que melhorariam significativamente meu fluxo de desenvolvimento.

## 4. Git e Github

Simplesmente indispensável. Todos os produtos que desenvolvemos na Giran são versionados pelo Git, nós utilizamos também o Github que parafraseando um [amigo](https://twitter.com/rodolfospalenza), que até hoje não postou nada no blog dele: "Todo desenvolvedor deveria conhecer o Github e ter uma conta lá".

## 5. Terminal

Depois de alguns meses usando o ZSH, por meio de um pacote de script providos pelo projeto [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh), estou de volta ao Bash. Tive alguns problemas misteriosos utilizando os scripts do oh-my-zsh então resolvi voltar ao Bash, com o auxílio de um [outro pacote de scripts](https://github.com/revans/bash-it) deixei-o do jeito que eu queria.

Depois de anos utilizando sistemas Unix Like - antes eu usava Linux (Slackware, Archlinux, Debian, Ubuntu) e hoje MacOSX - não consigo mais utilizar um SO que não tenha um terminal descente.

## 6. Evernote (GTD)

O [Evernote](http://evernote.com) ganhou minha admiração, eu praticamente anoto tudo que julgo importante nele.

Na Giran temos uma reunião diária, chamamos de [Daily](http://improveit.com.br/scrum/daily_scrum), nela repassamos tudo que fizemos no dia anterior e o que faremos no dia de hoje bem como os impedimentos que ocorreram até o momento.

Um dos usos que faço do Evernote é anotar o que tenho feito no meu dia de trabalho, com isso conseguirei lembrar o que precisarei dizer na Daily do dia seguinte, bem como me planejar para o dia corrente. A medida que as solicitações vão chegando eu vou colocando na minha lista de coisas a fazer, conforme vou fazendo eu vou marcando como feito e tocando para o próximo da lista.

O Evernote se tornou tão útil pra mim que o utilizo em minha vida pessoal e demais atividades que tenho fora do meu trabalho.

## 7. Monitor Externo

Nunca tinha pensando que fosse tão bom e produtivo ter um monitor externo.

A possibilidade de distribuir janelas e visualiza-las ao mesmo tempo sem perda de informação é fantástico! Isso me ajuda muito na produtividade. Costumo abrir um terminal (iTerm2) em fullscreen, dividi-lo com tmux, e abrir o vim, visualizar os logs dos servidores, executar comandos, abrir o navegador e ainda sobra espaço. Tudo isso sem precisar ficar fazendo _"ALT + TAB"_.

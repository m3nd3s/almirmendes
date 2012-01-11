--- 
layout: post
title: "Super R\xC3\xA1pida: Validando sintaxe PHP no Vim"
wordpress_id: 269
wordpress_url: http://www.almirmendes.net/?p=269
date: 2010-05-16 15:14:46 -03:00
---
<a href="http://www.almirmendes.net/wp-content/images/vim_logo.png"></a>

<img class="alignleft" title="Vim" src="http://www.almirmendes.net/wp-content/images/vim_logo.png" alt="Vim" width="128" height="128" />Amigos, confesso que fiquei mais que duas semanas sem postar algo. Acontece que estou um tanto ocupado estudando algumas <em>"paradas"</em>, especialmente a framework Code Igniter.

Mas para não passar em branco queria compartilhar uma dica que vi há algum tempo, e utilizo constantemente, no Vim <em>(Sim! Eu uso o Vim para desenvolvimento)</em>, e se você também usa, ou quer usar, segue a dica.

Edite seu arquivo <em><strong>.vimrc</strong></em> e adicione ao final dele a linha abaixo:
[cc lang="vim">]﻿﻿map  :!php -l %[/cc]
Salve e pronto, está feito! Agora quando estiver codificando e quiser testar se há algum erro de sintaxe no código basta pressionar CTRL+B <em>(é pra isso que serve o "&lt;C-B&gt;" acima)</em> que o comando php será chamado para testar a sintaxe passando como argumento o arquivo atual. É importante ressaltar que o comando php faz parte do pacote php-cli que deve estar instalado em seu GNU/Linux.

Assim que eu tiver algo mais <em>"irado"</em> para publicar eu prometo que compartilho com vocês. Inté+

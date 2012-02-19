--- 
layout: post
title: "Função HtmlEntities() para Vim"
wordpress_id: 335
wordpress_url: http://www.almirmendes.net/?p=335
date: 2010-06-29 21:39:01 -03:00
---
Minha IDE de desenvolvimento preferida sem sombra de dúvidas é o Vim (MacVim, Gvim, etc..). Desde que voltei a ter o desenvolvimento como foco do meu trabalho que voltei a usá-lo com mais frequência - diga-se de passagem diariamente!

No momento estou desenvolvendo aplicações Web em PHP, e consequentemente tenho que usar alguns códigos HTMLs nas aplicações (views). Como boa prática não é bom colocar caracteres especiais (cedilhas, vogais acentuadas, etc) diretamente no HTML, pra isso são utilizados os entities dos caracteres em questão. Só que é muito custoso, lembrar dos entities e também digitá-los em tempo de codificação. Pelo menos eu acho um saco ficar digitando os entities, fora que volta e meia acontece de um sair errado.

Bem, pensando nisso e no poder que o Vim lhe permite, eu criei uma função - que adicionei no meu .vimrc - que faz a conversão dos caracteres e ainda mapeei ela para ser executada ao precisar uma tecla de atalho. Ficou "supimpa"!

Abaixo segue o código que adicionei ao meu .vimrc, é claro que você pode extendê-la e adicionar mais funcionalidades nela, inclusive peço que compartilhe da mesma forma que fiz.

Então vamos lá, abra o seu arquivo ~/.vimrc e adicione o código exibido abaixo, logo após salve e está pronto para uso:

[cc lang="vim"]
" Converte os caracteres especiais para suas respectivas
" entidades em HTML
function HtmlEntities()
   " Vogais com acento agudo
   silent s/á/\&aacute;/eg
   silent s/é/\&eacute;/eg
   silent s/í/\&iacute;/eg
   silent s/ó/\&oacute;/eg
   silent s/ú/\&uacute;/eg

   " Vogais com acento circunflexo
   silent s/â/\&acirc;/eg
   silent s/ê/\&ecirc;/eg
   silent s/î/\&icirc;/eg
   silent s/ô/\&ocirc;/eg
   silent s/û/\&ucirc;/eg

   " Vogais com til
   silent s/ã/\&atilde;/eg
   silent s/õ/\&otilde;/eg

   " C com cedilha
   silent s/ç/\&ccedil;/eg
endfunction

" Mapeamento da tecla através do atalho CTRL+H
map <silent> <C-H> :%call HtmlEntities()<CR>
[/cc]

Agora fique a vontade para codificar e colocar os caracteres acentuados do jeito que você sempre fez, depois basta entrar no modo de comando e digitar CTRL+H e veja a mágica acontecer! It's wonderful!

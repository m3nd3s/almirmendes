--- 
layout: post
title: Compartilhando o mouse e teclado com Synergy
wordpress_id: 158
wordpress_url: http://www.almirmendes.net/?p=158
date: 2009-12-04 15:04:20 -02:00
---
<p style="text-align: center;"><img class=" aligncenter" title="Synergy" src="http://synergy2.sourceforge.net/images/logo.gif" alt="Synergy" width="216" height="77" /></p>
O Synergy é uma ferramenta que permite o compartilhamento de um único conjunto de teclado e mouse entre vários computadores, mesmo que utilizando sistemas operacionais diferentes sem a necessidade de um hardware especial para isso. Se você conhece o equipamento denominado KVM, imagine que o Synergy fará praticamente o mesmo que o KVM faz.
<p style="text-align: center;"><img class=" aligncenter" title="KVM" src="http://www.sb.fsu.edu/~xray/Images/kvm-switch.jpg" alt="KVM permite utilizar mouse e teclado em várias CPUs" width="300" height="300" /></p>
O que o Synergy faz é utilizar-se da rede TCP/IP para redirecionar o uso do teclado e mouse para outra máquina, bastando pra isso mover o cursor para uma das extremidade do seu monitor, claro que isso deve ser configurado. Portanto é necessário configurar o Synergy de modo a informá-lo em que posição estão as máquinas.

Atualmente o Synergy roda tanto em SOs da Microsoft quanto em Unix e MAC OS. Aqui eu recomendo uma visita à página oficial do projeto <a title="Synergy" href="[http://synergy2.sourceforge.net" target="_blank">[http://synergy2.sourceforge.net</a>] para obter maiores detalhes.
<h2>Instalação</h2>
Como de costume, você pode instalar os pacotes do software para a sua distribuição, ou fazer a instalação manual a partir dos fontes. Não irei abordar a instalação manual, se você for fazer isso consulte a documentação que vem junto com os fontes do Synergy.
<h3>Archlniux</h3>
[cc lang="bash"]# pacman -S synergy[/cc]
<h3>Debian</h3>
[cc lang="bash"]# apt-get install synergy[/cc]
<h3>Slackware</h3>
<em>Utilize os Slackbuilds em: http://slackbuilds.org/repository/13.0/desktop/synergy-plus/</em>

Uma vez instalado o Synergy, basta configurar.
<h2>Configuração do Server</h2>
O Synergy tem dois binários executáveis, o servidor e o cliente. Chamaremos de servidor a máquina que tem o mouse e o teclado que serão compartilhados entre as demais estações.

Utilize a configuração abaixo como modelo, salve-a com o nome .synergy.conf no seu diretório home:
[cc lang="bash"]# Aqui devem vir os hosts que serão usados para compartilhar
# o mouse e teclado, o nome deve ser o hostname da máquina.

section: screens
servidor:
cliente:
end

# Em links nós definimos as posições em que esses screens irão ficar.
# As posições possíveis são: left, right, up ou down. Cada posição deve
# ser seguida pela screen definida acima.
# Em nosso caso a máquina que irá compartilhar o mouse e teclado está
# a esquerda, e o cliente, no caso um notebook, a direita.

section: links
servidor:
right = cliente
cliente:
left  = servidor
end

# Na sessão aliases nós iremos passar o endereço IP, ou nome (DNS),
# das screens configuradas. É dessa forma que o synergy consegue
# manipular as demais máquinas.

section: aliases
servidor:
192.168.0.5
cliente:
192.168.0.6
end[/cc]
Uma vez salvo o arquivo, basta rodar o executável do synergy servidor, rode-o com o seu usuário mesmo, NÃO é preciso usar o administrador do sistema para isso.
[cc lang="bash"]$ synergys --daemon[/cc]
<h2>Configuração do Cliente</h2>
O cliente é mais fácil ainda, basta executar o comando abaixo:
[cc lang="bash"]$ synergyc -f 192.168.0.5[/cc]
Esse comando irá executar o synergy client em foreground (-f) conectando ao servidor 192.168.0.5. Agora basta mover seu mouse para direita e quando ele atingir a extremidade direita do seu monitor o mouse, e o controle do teclado, passarão para a máquina da direita, ou seja, o cliente.
<h2>Agradecimentos</h2>
Especialmente ao meu amigo <a title="Blog do Renato Cunha" href="http://valedotrovao.com/" target="_blank">Trovão,</a> que me mostrou essa ferramenta pela primeira vez. Vlw Trovão.
<h2>Novidades</h2>
Existe também o synergy+ [<a title="Synergy+" href="http://code.google.com/p/synergy-plus/" target="_self">http://code.google.com/p/synergy-plus/</a>], que me parece ser um fork ou mesmo a continuação do projeto original, já que utilizam os mesmos parâmetros nos comandos e configuração.
<p style="text-align: center;"><img class="aligncenter" title="Synergy+" src="http://synergy-foss.org/img/splash.jpg" alt="" /></p>

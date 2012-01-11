--- 
layout: post
title: VMWare Server 1.0.10 e Kernel Linux 2.6.32.x
wordpress_id: 240
wordpress_url: http://www.almirmendes.net/?p=240
date: 2010-04-16 21:20:48 -03:00
---
Essa dica é para os que ainda não aderiram ao novo VMWare Server 2.0 e ainda utilizam o saudoso VMWare Server 1.0.x e  precisam atualizar o kernel para uma versão mais nova. Abaixo segue uma dica de como fazer a instalação do VMWare Server 1.x sobre o kernel 2.6.32.
<p style="text-align: center;"><img class="aligncenter" title="VMWare Server" src="http://www.scherm.com.br/site_antigo/VMwareLogo.jpg" alt="VMWare Server" width="400" height="157" /></p>
A minha experiência foi em um Debian Lenny 5.0.4 <em>(servidor de um cliente)</em>, kernel 2.6.32.9 e VMWare Server 1.0.10. Eu já tinha um kernel compilado neste servidor, isso porque o hardware era muito novo e precisava de compilação de kernel mais recente que o padrão de instalação do Debian para suportar o hardware em questão.

Mesmo se você já tiver um kernel 2.6.32.x instalado será necessário recompilar ele novamente <em>(foi o que fiz)</em>, isso  é necessário porque é preciso fazer um pequeno "hacking" no kernel manualmente.

A idéia original surgiu a partir de uma dica encontrado no fórum da comunidade do VMWare (<a title="VMWare Communities" href="http://communities.vmware.com/thread/242415" target="_blank">http://communities.vmware.com/thread/242415</a>) que foi publicado por um "carinha" de codnome <strong>goldeneye*007</strong>. Dados os devidos créditos vamos a dica:

Começo do princípio de que você:
<ol>
	<li>Saiba compilar um kernel e que já tenha baixado o kernel 2.6.32.x, esteja pronto e devidamente configurado;</li>
	<li>Que tenha baixado o VMWare Server 1.0.x.</li>
</ol>
Para que o VMWare Server possa ser instalado é necessário alterar, manualmente, o arquivo <strong>arch/x86/kernel/init_task.c</strong> e adicionar a seguinte linha ao final dele:
[cc lang="c"]EXPORT_UNUSED_SYMBOL(init_mm);[/cc]
Realizado esse procedimento  siga com a compilação e instalação do kernel conforme já esteja acostumado (ou não) a fazer. Reinicie o sistema e selecione o kernel que acabou de compilar (claro!).

Agora partimos para o VMWare Server. Baixe o patch disponível <a title="Patch Kernel 2.6.32.x" href="http://www.insecure.ws/warehouse/vmware-update-2.6.32-5.5.9.tar.bz2">AQUI</a> e o salve em seu sistema de arquivos. Caso não tenha o VMWare Server instalado faça-o agora, o processo de instalação irá parar em um erro durante a compilação dos módulos usados pelo VMWare, isso é esperado.

Se já estiver com o VMWare instalado, ou tenha feito o processo de tentativa de instalação acima citado, descompacte o patch baixado, entre na pasta que foi criada e - como usuário root - execute o comando ./runme.pl:
[cc lang="bash"]# cd vmware-update-2.6.32-5.5.9
# ./runme.pl[/cc]
Feito isso basta seguir os procedimentos sugeridos pelo script e ser feliz.

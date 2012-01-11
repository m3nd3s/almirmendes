--- 
layout: post
title: "VMWare: Redimensionando discos virtuais"
wordpress_id: 255
wordpress_url: http://www.almirmendes.net/?p=255
date: 2010-04-29 20:17:09 -03:00
---
Certa vez eu precisei redimensionar um disco virtual de uma máquina virtual rodando sobre VMWare Server 1.0. Até então desconhecia uma forma de fazê-lo de forma elegante, então quando eu tinha uma máquina virtual com um sistema GNU/Linux era mais fácil apenas adicionar um novo HD e usá-lo no LVM.

Entretanto dessa vez a minha necessidade era redimensionar um disco virtual de uma máquina virtual MS Windows. O espaço planejado inicialmente para a unidade "C" estava quase totalmente ocupada, impedindo a instalação de novos softwares. A solução então era realmente redimensionar o disco.

Com uma breve pesquisa fiquei sabendo do <em>vmware</em>-<em>vdiskmanage, </em>que é usado para administrar os discos virtuais do VMWare e permite o redimensionamento do disco virtual. A sintaxe de uso do comando, para redimensionar o disco virtual, segue o padrão abaixo:
[cc lang="bash"]# vmware-vdiskmanager -x 10G DiscoSO.vmdk[/cc]
Onde tem 10G é o espaço total que a partição deverá ter ao final do processo que pode levar alguns minutos até ser finalizado. Ao final do processo, se tudo correr bem, você terá o novo disco já redimensionado.

Faça o boot da VM e aguarde o carregamento. Agora vem a parte mais chata, o espaço adicionado ao disco será reconhecido como <em>espaço não particionado</em> pelas ferramentas de administração de disco do MS Windows. Nesse ponto você terá que usar de alguma ferramenta capaz de expandir partições NTFS (ou fat). Eu tentei o parted e o ntfsresize, ambos para ambiente GNU/Linux, via LiveCD, entretanto ambos não tinham suporte a redimensionar as partições NTFS em questão. Uma boa pesquisa no Google e você achará ótimas opções gratuitas para o próprio MS Windows, no meu caso eu usei o ASEUS Partition Master (http://www.partition-tool.com/personal.htm).

Se sua VM tiver um sistema GNU/Linux tudo fica muito mais fácil, ao expandir o disco apenas utilize o particionador de sua preferência e crie nova(s) partição(ões) com o espaço adicional.

Quem sabe em um novo artigo eu publique algo sobre LVM, já que toquei no assunto de partições mesmo! ;-)

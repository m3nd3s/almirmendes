---
layout: post
title: "Instalando Nginx com RVM para aplicações Rails"
date: 2012-07-27 13:05
comments: true
categories: linux rvm nginx rails ruby
published: true
---

Olá pessoal! Depois de muito tempo sem um post, eu resolvi fazer algo que estava no meu dashboard há um bom tempo, explicar o básico para se levantar uma aplicação Rails e Nginx em um servidor Linux. 

Minha intenção com o post é passar os caminhos básicos de como configurar o Nginx, o Passenger e o RVM em um servidor Linux. O processo é relativamente simples.

Antes de começar o processo de instalação é necessário que você possua acesso de administrador do sistema, ou seja, acesso ao usuário _root_. Caso você não possua esse nível de acesso os comandos abaixo não darão certo.

Algumas distribuições não permitem o acesso direto ao usuário _root_, exigindo que você tenha uma conta de usuário normal e só então, a partir dele, mudar o nível de acesso para o _root_, isso normalmente é feito através do comando `sudo`. Se for o seu caso sugiro rodar o comando `sudo su -` que fará você mudar o nível de privilégios para administrador do sitema, aí é só seguir os passos abaixo.

## Instalando o RVM

O processo de instalação do RVM não possui muitos mistérios, basta seguir [o processo de instalação disponível no site do RVM](https://rvm.io/rvm/install/). Mas para que você não tenha dúvidas segue a linha a ser executada:

``` bash Instalando o RVM
curl -L https://get.rvm.io | bash -s stable --ruby
```

Este comando fará a instalação do RVM no sistema, e logo em seguida a instalação da a última versão do ruby disponível, no momento que escrevo esse post a versão mais atual é a **1.9.3-p194**. 

A instalação do RVM requer o uso do `curl`, portanto é preciso ter ele instalado, verifique como instalar esse software em sua distribuição/versão de Linux.

Caso ocorra algum erro na instalação do ruby é bem provável que seja pela ausência de alguma dependência na distribuição utilizada, para fazer um levantamento e identificar se falta algo rode o comando `rvm requirements`. Siga os procedimentos informados e após terminar tente novamente instalar o `ruby`:

``` bash Instalando o ruby manualmente
rvm install 1.9.3 #ou a versão que deseja
```

## Instalando o Passenger

Esse talvez seja o passo mais fácil. O passenger é uma gem que por sua vez possui um script que auxilia em todo o processo, como estamos fazendo a instalação em um ambiente servidor nós podemos instalar a gem sem os arquivos de documentação:

``` bash Instalando o Passenger
gem install passenger --no-ri --no-rdoc
```

Pronto, agora já temos o passenger instalado. Entretanto ele sozinho não fará muita coisa por você, ou melhor, por sua aplicação. Vamos agora instalar o Nginx.

## Instalando o Nginx

Infelizmente não podemos utilizar o Nginx provido pela distribuição Linux que você está usando, isso porque o Nginx não possui o suporte a módulos, algo que o Apache tem, que seria a possibilidade de instalar o Nginx e depois apenas os módulos que necessários (php, ruby, etc.). Para o nosso caso será necessário (re)compilar o Nginx habilitando o suporte ao Passenger, é justamente isso que vamos abordar no próximo tópico.

### Instalando o Nginx com suporte ao Passenger (usando o assistente)

Nós utilizaremos o instalador provido pela gem `passenger`, esse script fará todo o trabalho sujo por você, baixando o nginx, configurando e compilando. Esse processo é recomendado para aqueles que estão começando e querem algo funcional de forma simples. Vamos lá então:

``` bash Instaladando o Nginx com suporte ao passenger
passenger-install-nginx-module
```

O script fará uma série de perguntas, vou documentar cada uma delas e explicar para que você se sinta seguro `;)`. 

Logo no início será apresentado um texto informativo sobre o que será realizado durante o processo de instalação, nessa primeira parte será solicitado que você pressione `<ENTER>` para continuar, ou `<CTRL>-C` caso tenha se arrependido e queira abortar a instalação. **É óbvio que vamos continuar né!** `:P`, senta o dedo aí no `<ENTER>`.

Logo em seguida o script fará um checklist sobre todas as dependências necessárias para compilar o Passenger e o Nginx, entre os itens verificados estão: compilador, make, curl ou wget, headers do ruby (bibliotecas necessárias para compilação), rubygems, rack, openssl, zlib, etc. Caso algum deles esteja faltando o script fará o alerta e mostrará o que fazer para resolver as dependências.

Se for o seu caso, instale as dependências e depois volte a executar o comando `passenger-install-nginx-module` novamente.

Após o checklist de dependências o script solicitará qual o método você utilizará para instalar o Nginx + Passenger:

``` text Questionamento sobre qual processo será utilizado para instalar o Nginx + Passenger
Automatically download and install Nginx?

Nginx doesn't support loadable modules such as some other web servers do,
so in order to install Nginx with Passenger support, it must be recompiled.

Do you want this installer to download, compile and install Nginx for you?

 1. Yes: download, compile and install Nginx for me. (recommended)
    The easiest way to get started. A stock Nginx 1.0.10 with Passenger
    support, but with no other additional third party modules, will be
    installed for you to a directory of your choice.

 2. No: I want to customize my Nginx installation. (for advanced users)
    Choose this if you want to compile Nginx with more third party modules
    besides Passenger, or if you need to pass additional options to Nginx's
    'configure' script. This installer will  1) ask you for the location of
    the Nginx source code,  2) run the 'configure' script according to your
    instructions, and  3) run 'make install'.

Whichever you choose, if you already have an existing Nginx configuration file,
then it will be preserved.
```

Selecione a opção 1 e pressione `<ENTER>`. Nesta opção será feito o download e compilação do Nginx com suporte ao Passenger pelo próprio script. Logo Após será feito um novo questionamento, desta vez sobre qual será o local onde o Nginx será instalado. Eu prefiro escolher um local diferente por questões de gosto e costume, em meus processos de instalação eu utilizo o path `/usr/local/nginx`, fique a vontade para escolher qual deles utilizar.

``` text Onde instalar o Nginx
Where do you want to install Nginx to?

Please specify a prefix directory [/opt/nginx]: /usr/local/nginx
```

Faça a sua escolha e pressione `<ENTER>` para dar início a compilação, agora é só esperar finalizar o processo.

Ao finalizar a compilação e instalação do Nginx o script exibe alguns parâmetros que devem ser definidos na configuração do Nginx para ativar o passenger, nós não precisamos nos preocupar com isso agora pois o script de instalação já injetou essas diretivas no arquivo de configuração do nginx, mas vale a pena registrar para não ter dúvidas:

``` text Nginx instalado, diretivas de configuração para suporte ao Passenger
Nginx with Passenger support was successfully installed.

The Nginx configuration file (/usr/local/nginx/conf/nginx.conf)
must contain the correct configuration options in order for Phusion Passenger
to function correctly.

This installer has already modified the configuration file for you! The
following configuration snippet was inserted:

  http {
      ...
      passenger_root /usr/local/rvm/gems/ruby-1.9.3-p194/gems/passenger-3.0.15;
      passenger_ruby /usr/local/rvm/wrappers/ruby-1.9.3-p194/ruby;
      ...
  }

After you start Nginx, you are ready to deploy any number of Ruby on Rails
applications on Nginx.
```

Pressione `<ENTER>` e outra mensagem informativa será exibida, desta vez é exibido um trecho de configuração da seção `server` dos arquivos de configuração do Nginx, essa seção é utilizada justamente para configurar uma aplicação/site no Nginx, **esta não é inserida automaticamente**, precisaremos setar isso quando da configuração de nossa aplicação.

## Organizando a instalação

Vamos agora dar uma organizada para termos menos trabalho no futuro, até para melhorar a manutenção. Como é padrão das distribuições linux os arquivos de configuração devem ficar no path `/etc`, sendo assim ficaria melhor se a configuração do Nginx ficasse em `/etc/nginx`, vamos criar um link simbólico dos arquivos de configuração do Nginx para o `/etc/nginx`:

``` bash Criando link simbólico do Nginx para o /etc/
ln -s /usr/local/nginx/conf /etc/nginx
```

Outra melhoria que podemos fazer é colocar o binário do nginx em um path globalmente reconhecido pelo linux, para isso vamos criar outro link simbólico:

``` bash Criando link simbólico do binário do nginx
ln -s /usr/local/nginx/sbin/nginx /usr/local/sbin/nginx
```

## Configurando o Nginx

O Nginx é instalado com um arquivo default de configuração, não vou cobrir todo esse processo, no lugar eu sugiro que você baixe e use o arquivo de configuração abaixo:

{% gist 3334030 nginx.conf %}

A seguir vamos criar algumas pastas para organizar melhor os arquivos de configuração:

``` bash Criando a pasta conf.d, sites-enabled e sites-available
mkdir /etc/nginx/conf.d
mkdir /etc/nginx/sites-enabled
mkdir /etc/nginx/sites-available
```
## Configurando seu domínio

Pronto, quase tudo configurado, falta agora configurar o Nginx para responder pelo domínio de seu site, para isso usaremos a diretiva `server`, vamos utilizar como exemplo o meu domínio almirmendes.com. Vamos criar um arquivo em `/etc/nginx/sites-available/` com o nome do seu domínio (o nome não importa, pode ser qualquer um):

``` bash Criando arquivo de configuração para o domínio
vim /etc/nginx/sites-available/almirmendes.com
```

Eu tenho, no Gist abaixo, uma configuração que você pode utilizar como exemplo, apenas lembre-se de trocar as entradas que tiverem **almirmendes.com** pelo seu domínio:

{% gist 3482847 %}

Agora vamos fazer um link simbólico do arquivo `almirmendes.com` para a pasta `/etc/nginx/sites-enabled/. Se reparar no arquivo de configuração acima, no gist 3482847, ela é a única que está sendo lida pelo Nginx, esta é a forma que temos para ativar uma configuração nova de site. Com isso habilitaremos o site:

``` bash Habilitando a configuração do domínio
ln -s /etc/nginx/sites-available/almirmendes.com /etc/nginx/sites-enabled/almirmendes.com
```

Se algum dia precisar desativar o site basta remover o link simbólico e pronto em `/etc/nginx/sites-enabled/almirmendes.com`. Você ainda terá o arquivo de configuração intacto em `/etc/nginx/sites-available`.

Para testar a configuração use o seguinte comando:

``` bash Testando a configuração do nginx
nginx -t
```

Se no resultado do comando acima aparecer algo semelhante ao exibido abaixo é sinal de que está tudo correto, agora só falta inicializarmos o Nginx `;)`:

``` bash Sintaxe testada pelo Nginx
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful
```

## Script de inicialização do Nginx

Por fim falta só adicionar ao sistema o script de inicialização do Nginx. Sugiro que baixe o que está disponível [neste link](https://gist.github.com/3506074) e salve-o em `/etc/init.d/nginx`. :

``` bash Inicializando o Nginx
chmod +x /etc/init.d/nginx # permissão de execução para o script
service nginx start #inicializa o nginx
```

Existem inúmeras outas informações a serem adicionadas ao post, entretanto não queria deixá-lo ainda maior. Espero que ajude você a configurar o Nginx, qualquer coisa estamos a disposição. Abraços!

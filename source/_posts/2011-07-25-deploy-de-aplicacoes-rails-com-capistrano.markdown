--- 
layout: post
title: "Deploy de aplica\xC3\xA7\xC3\xB5es Rails com Capistrano"
wordpress_id: 493
wordpress_url: http://www.almirmendes.com/?p=493
date: 2011-07-25 18:34:50 -03:00
---
Me lembro do tempo que eu perdia fazendo subir minhas aplicações PHP para servidor de produção (deploy): tinha que criar o banco de dados, fazer um <em>dump</em> do banco de dados de desenvolvimento para carregar o banco de dados de produção, checar as permissões dos paths utilizados para upload, etc.

Quanto tinha atualização para fazer era uma preocupação danada, eu precisava checar quais arquivos foram atualizados para só subir estes e assim não correr o risco de sobrescrever alguma configuração própria do ambiente de produção.

<a href="http://www.almirmendes.com/2011/07/25/deploy-de-aplicacoes-rails-com-capistrano/100px-ruby_on_rails_logo/" rel="attachment wp-att-526"><img src="http://www.almirmendes.com/wp-content/uploads/2011/07/100px-Ruby_on_Rails_logo.jpg" alt="" title="Ruby on Rails" width="100" height="119" class="alignleft size-full wp-image-526" /></a>Há algum tempo eu parei de desenvolver aplicações em PHP para trabalhar com o framework <a href="http://rubyonrails.org/" title="Ruby on Rails" target="_blank">Ruby on Rails</a>, aproveitando a deixa, tenho uma palestra onde conto um pouco como está sendo essa migração e o que ganhei com isso. Dentre as facilidades que ganhei ao migrar para o framework Rails está o deploy - que significa implantação em inglês - de aplicações via ferramenta chamada <a href="https://github.com/capistrano/capistrano" title="Capistrano" target="_blank">Capistrano</a>.

O Capistrano é uma ferramenta (gem) para deploy de aplicações web. Inicialmente utilizada para deploy de aplicações Ruby on Rails ela também pode ser personalizada para fazer deploy de aplicações não Rails. O Capistrano é tipicamente instalado em uma estação de trabalho e usado para implantar o código fonte de sua aplicação, via um gerenciador de código fonte (SCM), em um ou mais servidores previamente configurados.

Para utilizar o Capistrano tenha em mente que:
<ul>
	<li>É necessário acesso SSH ao servidor de produção, onde será realizado o deploy de sua aplicação. O Capistrano não suporta FTP ou telnet;</li>
	<li>O servidor de produção precisa ter um shell compatível com o padrão POSIX, ou seja, precisa ter um: bash, sh, etc. Resumidamente não é aconselhável para servidores MS Windows, mas acredito que seja possível se você tiver força de vontade e instalar um pacote POSIX em seu servidor MS Windows;</li>
	<li>Trabalhe com chaves SSH, é muito mais prático e fácil, permitindo que o processo fique mais automátizado.</li>
</ul>
O Capistrano possui um arquivo chamado [cci]Capfile[/cci]. Este arquivo é responsável por incluir as bibliotecas necessárias, bem como os helpers utilizados para configurar o deploy de sua aplicação.

<h3>Instalação</h3>
Por se tratar de uma gem a instalação é muito simples e segue o padrão já conhecido:

[cc lang="teraterm"]$ gem install capistrano[/cc]

Ou se preferir adicione-o ao seu projeto Rails por meio do arquivo Gemfile:

[cc lang="ruby"]group :development
    gem 'capistrano'
end[/cc]

<h3>Capificação</h3>
O primeiro passo após instalar o Capistrano é "capificar" sua aplicação. Este processo consiste em transformar sua aplicação gerenciável pelo Capistrano. O processo é simples, rode o comando abaixo na raiz de sua aplicação:

[cc]$ cd my_app
$ capify .[/cc]

Este comando criará dois arquivos em sua aplicação, o primeiro é o já citado [cci]Capfile[/cci], este é o arquivo responsável por carregar as bibliotecas necessárias ao Capistrano.

O segundo arquivo é gerado o [cci]config/deploy.rb[/cci], e este é o arquivo que iremos utilizar para configurar nosso deploy. Em geral este será o único arquivo que precisaremos alterar para configurar nosso deploy.

<h3>Configuração</h3>
Conforme já mencionado, a configuração é feita através do arquivo [cci]config/deploy.rb[/cci], o formato é muito semelhante ao [cci]Rakefile[/cci]. O primeiro passo é informar o nome de nossa aplicação, fique a vontade para escolher um nome:

[cc lang="ruby"] set :application, "almirmendes_blog"[/cc]

Agora precisamos informar ao Capistrano onde reside o código fonte de nossa aplicação, para este exemplo estou considerando que minha aplicação está hospedada no <a href="http://github.com" title="Github" target="_blank">Github</a>:

[cc lang="ruby"]

set :repository, "git@github.com:m3nd3s/almirmendes_blog.git"
set :scm, "git"

[/cc]

Agora vamos configurar o caminho onde a aplicação será implantada/instalada:

[cc lang="ruby"] set :deploy_to, "/var/www/almirmendes" [/cc]

Além do path/caminho nós precisamos informar ao Capistrano o(s) endereço(s) de nosso servidor de produção, segue um exemplo:

[cc lang="ruby"]

role :app, "almirmendes.com"
role :web, "almirmendes.com"
role :db, "almirmendes.com", :primary => true

[/cc]

Nesse ponto pode surgir uma dúvida: <em>"Porque preciso informar três vezes o endereço?"</em>. Eu também fiquei com essa dúvida pela primeira vez, mas a explicação é muito boa e traz consigo outro recurso do Capistrano.

Perceba que o atributo é diferente para cada um deles, isto porque em alguns casos sua aplicação está distribuída em servidores diferentes - no meu caso estou usando o mesmo servidor para a aplicação, o banco de dados e servidor web - e possivelmente você queira definir tarefas para serem executadas apenas em um ou outro servidor. Resumidamente, o Capistrano lhe fornece a opção de definir comandos/tarefas para serem executados em um servidor específico, e não em todos.

Como em nosso exemplo estamos usando o mesmo servidor para tudo, existe uma configuração rápida para substituir as linhas citadas acima, assim a configuração mais clara e simples. Substitua as três linhas acima, caso queria, pela linha abaixo:

[cc lang="ruby"]

server "almirmendes.com", :app, :web, :db, :primary => true

[/cc]

Precisamos informar também o usuário que será utilizado durante o processo de deploy. É importante que este usuário tenha permissão de escrita na pasta onde a aplicação será instalada:

[cc lang="ruby"]

set :user, "almir"
set :use_sudo, false

[/cc]

Por padrão o Capistrano tentará executar certos comandos com o [cci]sudo[/cci]. Se você estiver fazendo deploy de sua aplicação em um servidor compartilhado é muito provável que você não tenha acesso de superusuário e tão pouco o [cci]sudo[/cci] configurado, portanto vamos configurar o Capistrano para não utilizar o [cci]sudo[/cci] - conforme visto acima.

Neste ponto já temos o que é suficiente para um deploy "saudável", entretanto gostaria de passar mais algumas opções que podem ajudar:

[cc lang="ruby"]

# Utilizar Capistrano junto com RVM
$:.unshift(File.expand_path('./lib', ENV['rvm_path'])) # Add RVM's lib directory to the load path.
require "rvm/capistrano"                  # Load RVM's capistrano plugin.
set :rvm_ruby_string, '1.9.2'

# Mais configurações
set :keep_releases, 5
ssh_options[:forward_agent] = true

[/cc]

As primeiras três linhas são referentes configuração para permitir o deploy em servidores configurados com o RVM - Ruby Version Manager - e informar qual a versão do Ruby iremos utilizar no deploy. Já as duas outras linhas são: 


<ul>
    <li>A primeira, permite definir o número de releases que serão armazenados no servidor. Essa configuração permite que você possa manter versões anteriores de sua aplicação no servidor e com isso posssa realizar rollback caso seja necessário.</li>
	<li>A última linha é importântissima pois permite que o Capistrano utilize do recurso de forward agent do SSH, esse recurso permite que o SSH carregue sua chave, previamente configurada e carregada em sua estação de trabalho, para o servidor. Permitindo assim que de lá o Capistrano consiga acessar o repositório no Github.</li>
</ul>

<h3>Deploy</h3>
Agora chegou a hora de fazer o deploy de nossa aplicação, esse processo é feito em duas etapas: setup e o deploy propriamente dito. Antes, vamos checar se todas as dependências foram cumpridas:

[cc] cap deploy:check [/cc]

Se tudo correr bem, rode o comando setup para preparar o ambiente para o deploy:

[cc] cap deploy:setup [/cc]

O setup é necessário para criar a estrutura base que será utilizada para gerenciar os deploys, abaixo um exemplo da estrutura que é criada no [cci]setup[/cci]:

[cc]

[deploy_to]
[deploy_to]/releases
[deploy_to]/releases/20080819001122
[deploy_to]/releases/...
[deploy_to]/shared
[deploy_to]/shared/log
[deploy_to]/shared/pids
[deploy_to]/shared/system
[deploy_to]/current -> [deploy_to]/releases/20100819001122

[/cc]

Basicamente são duas pastas e um link simbólico. [cci]releases/[/cci] é a pasta que manterá os releases dos deploys já realizados. A cada deploy criado uma pasta será criada nesse diretório. A pasta [cci]shared/[/cci], como o nome já descreve, é utilizada para compartilhar configurações, logs e arquivos que devem ser mantidos mesmo após um deploy. Dentre eles temos os logs, pids e uploads.

Antes de fazer o deploy nós precisamos criar o banco de dados e seus respectivos acessos e permissões. Esse processo deve ser feito manualmente e imagino que você saiba como fazer isto. 

Após criar o banco de dados nós precisamos configurar o [cci]database.yml[/cci] que será utilizado no servidor. Uma vez configurado envio para a pasta [cci]shared/[/cci] no servidor de produção e adicione a seguinte task ao seu arquivo [cci]config/deploy.rb[/cci]:

[cc lang="ruby"]
after :deploy, 'deploy:database'
namespace :deploy do
    task :database, :roles => :app do
        run "cp #{deploy_to}/shared/database.yml #{current_path}/config/"
    end
end
[/cc]

Essa task será executada assim que a task denominada [cci]:deploy[/cci] for finalizada e copiará o arquivo [cci]database.yml[/cci] para o path [cci]config/[/cci]. Hora de fazer o deploy. Para fazer o deploy rode o comando:

[cc]cap deploy[/cc]

Uma série de comandos será executado, ao final, se nenhum erro ocorrer, sua aplicação terá uma estrutura semelhante à exibida acima e o deploy terá sido executado com sucesso.

Entretanto, acredito que ainda há mais um passo a ser feito, uma vez realizado o deploy, o Capistrano precisa reinicializar a aplicação e normalmente ele faz isso reiniciando o servidor web. Mas sabemos que não é necessário reinicializar o servidor web para isso, bastaria atualizar a data de alteração do arquivo [cci]tmp/restart.txt[/cci] existente na sua aplicação. Vamos sobrescrever a tarefa responsável por isso (repare que o código está dentro do namespace :deploy):

[cc lang="ruby"]

namespace :deploy do
    task :restart, :roles => :app, :except => { :no_release => true } do
        run "cd #{current_path} && touch tmp/restart.txt"
    end
end

[/cc]

Caso necessário rode novamente o comando para deploy: [cci] cap deploy [/cci]. Pronto, aplicação implantada. Quando um deploy é realizado um link simbólico é criado dentro do caminho configurado para deploy, via diretiva [cci]deploy_to[/cci], de nome [cci]current[/cci]. O [cci]current[/cci] aponta para o último release criado.

O artigo ficou grande, mas espero que tenha informações úteis para lhe ajudar. Obrigado e até mais.

--- 
layout: post
title: "Introdução ao PDO - PHP Data Objects"
wordpress_id: 114
wordpress_url: http://www.almirmendes.net/?p=114
date: 2009-07-13 22:15:36 -03:00
---
<h3>Introdução</h3>
Olá amigos, em meu último artigo eu explanei um pouco sobre como utilizar a biblioteca ADOdbPHP para conexões com banco de dados. Essa ferramenta é muito utilizada por sistemas web devido as facilidades de utilização e implementação, bem como a agilidade no desenvolvimento que ela proporciona, sua principal característica é proporcional ao desenvolvedor uma "interface" única de manipulação de querys e de dados retornados do banco, independente de qual SGDB você utilize. É uma classe de abstração.

Pois bem, agora (já faz um tempinho) o PHP possui algo parecido, chamado de PDO (PHP Data Objects).  O PDO provê uma camada de acesso a dados, ou seja, ele funciona como uma interface para o desenvolvedor, assim como faz o ADOdbPHP só que com uma leve diferença, o PDO não é uma classe de abstração. Resumindo, você pode utilizar o mesmo conjunto de funções para se comunicar com o banco de dados escolhido.

Mas uma observação deve ser feita, a PDO não provê uma abstração do banco de dados, o que quer dizer que as SQLs devem ser construídas conforme o banco de dados escolhido.
<h3>Instalação</h3>
A PDO é provida no PHP 5.1, mas desde a versão 5.0 você pode utilizar ela através da extensão PECL.
<h4>Linux/Unix</h4>
Se for compilar o pacote ou fazer a instalação via código fonte, basta adicionar a diretiva --enable-pdo=shared --with-pdo-sqlite=shared para o comando ./configure. Caso já possua o PHP instalado, você pode lançar mão da instalação via PECL, basta executar o comando "pecl install pdo", e pronto, será gerada a extensão, depois é só configurar o php.ini adicionando a linha "extension=pdo.so" para habilitar o suporte.
Não se esqueça de reiniciar o Apache.
<h4>Windows</h4>
Em sistemas Windows fica mais fácil ainda habilitar o pdo, basta descomentar a linha referente a extensão. Normalmente ela vem comentada como no exemplo abaixo:
<pre lang="PHP">;extension=php_pdo.dll</pre>
Basta tirar o ";" para descomentar e reiniciar o Apache.
<h3>Utilizando a PDO</h3>
Agora que já estamos(supostamente) com tudo pronto para utilizar a PDO, vamos ver alguns exemplos:
<pre lang="PHP">
try {
    $dbh = new PDO('mysql:host=localhost;dbname=test', $user, $pass);
    foreach($dbh->query('SELECT * from FOO') as $row) {
        print_r($row);
    }
    $dbh = null;
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}

$conn = null;
</pre>
Nesse nosso exemplo, temos uma conexão e uma query de consulta ao banco, agora vamos explicar o que acontece: A string de conexão com o banco seque o padrão onde o primeiro campo é o driver utilizado para conexão, no nosso caso o "mysql", logo após vem as informações de host onde está o servidor de banco de dados que no nosso caso está na própria máquina (por isso o "localhost"), e o nome do banco de dados que no nosso caso é o "banco_teste".

Logo após a query é executada através do método "query", que retorna o resultado como um array, que por sua vez é trabalhado pelo foreach, sendo acessado através da variável $row_result.

Ao final temos a definição do objeto $conn para NULL.

Aos que necessitam ou querem usar conexões permanentes, um array de parâmetros pode ser passado, logo após a senha do usuário. Sendo assim linha que faz a conexão com o banco fica mais ou menos assim:
<pre lang="PHP">
$conn = new PDO('mysql:host=localhost;dbname=banco_teste', "meu_usuario", "minha_senha", array(
    PDO::ATTR_PERSISTENT => true
));
</pre>

Bem, como este é apenas um breve artigo introdutório, vamos ficar por aqui. Senão irei desanimar e não conseguirei postar o artigo todo.. rs, e lembre-se, em caso de dúvida, entrem na lista do <a target="_blank" href="http://www.phpes.org/lista-de-discussoes/">PHP-ES</a> e perguntem, estarei por lá para responder. ;)

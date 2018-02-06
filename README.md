# Exemplo de Pool de Conexão em PHP usando PDO

Exemplo de utilização:

```php
<?php
require_once './Connection.php';
require_once './PoolConnection.php';

try{
    $con1 = new Connection();
    $con2 = new Connection();
    
    $pooll = new PoolConnection();
    $pooll->addConnection($con1);
    $pooll->addConnection($con2);


    echo '<pre>';
    echo '<h2>Tentando pegar 1º conexão do Pool e buscando todos as empresas cadastradas</h2>';
    $connection1 = $pooll->getConnection();    
    $result = $connection1->query('SELECT * FROM companies', Connection::FETCH_OBJ);

    foreach($result as $row){
        print_r($row);
    }

    echo '<h2>Tentando pegar 2º conexão do Pool e buscando todos as empresas cadastradas</h2>';
    $connection2 = $pooll->getConnection();
    $result2 = $connection2->query('SELECT * FROM companies', Connection::FETCH_OBJ);    
    
    foreach($result2 as $row){
        print_r($row);
    }
    
    echo '<h2>Tentando pegar 3º conexão do Pool e buscando todos as empresas cadastradas</h2>';
    $connection3 = $pooll->getConnection();
    $result2 = $connection3->query('SELECT * FROM companies', Connection::FETCH_OBJ);
    
    foreach($result3 as $row){
        print_r($row);
    }    

} catch (Exception $e){
    echo $e->getMessage();
}
```


Resultado:

```php
Tentando pegar 1º conexão do Pool e buscando todos as empresas cadastradas
stdClass Object
(
    [id] => 17
    [email] => dev@tayron.com.br
    [logo] => 2996ba842dae4529a150.jpg
    [name] => Empresa A
    [site] => www.empresaa.com.br
    [telephone] => (31) 98888-9999
    [user_id] => 
    [city_id] => 5276
)
Tentando pegar 2º conexão do Pool e buscando todos as empresas cadastradas
stdClass Object
(
    [id] => 17
    [email] => dev@tayron.com.br
    [logo] => 2996ba842dae4529a150.jpg
    [name] => Empresa A
    [site] => www.empresaa.com.br
    [telephone] => (31) 98888-9999
    [user_id] => 
    [city_id] => 5276
)
Tentando pegar 3º conexão do Pool e buscando todos as empresas cadastradas
Nao ha nenhuma conexao disponivel
```
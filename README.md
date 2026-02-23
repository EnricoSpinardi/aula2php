# aula2php

Atividade
Incluir list e add para fornecedor conforme exemplo da aula (pasta fornecedor)
Editar o navbar
Guarde a atividade até que seja liberado o teams

#######################################


<?php
setlocale(LC_TIME, "pt_BR", "pt_BR.utf-8", "pt_BR.utf-8", 'portuguese');
date_default_timezone_set('America/Sao_Paulo');
?>
<!DOCTYPE html>
<html lang="pt-br">

<head>
    <?php include_once 'cabecalho.php'; ?>
</head>

<body>
    <?php include_once 'navbar.php'; ?>

    <div class="container mt-3">
        <?php
        $pagina = filter_input(INPUT_GET, 'p');
        if (empty($pagina)) {
            include_once 'home.php';
        } else {
            if (file_exists($pagina . '.php')) {
                include_once $pagina . '.php';
            } else {
                echo "Erro 404 - página não encontrada!";
            }
        }
        ?>
    </div>

    <?php include_once "scripts.php"; ?>
</body>

</html>

#######################################

<div class="alert alert-success" role="alert">
    <h3>Seja bem vindo</h3>
</div>

#######################################

<div class="alert alert-warning" role="alert">
    <h3>Adicionar categoria</h3>
</div>

<a href="?p=categoria/list" title="Listar Categorias">Voltar</a>

#######################################

<div class="alert alert-primary" role="alert">
    <h3>Listar categorias</h3>
</div>

<a href="?p=categoria/add" title="Add Categoria">+ Categoria</a>

#######################################

Outra versão do script

<?php

// Captura e sanitiza o parâmetro
$pagina = filter_input(INPUT_GET, 'p', FILTER_SANITIZE_SPECIAL_CHARS);

// Define páginas permitidas (lista branca)
$paginasPermitidas = [
    'index' => 'home.php',
    'home' => 'home.php',
    'sobre' => 'sobre.php',
    'contato' => 'contato.php',
    'produtos' => 'produtos.php'
];

// Página padrão
if (empty($pagina)) {
    $pagina = 'index';
}

// Verifica se está na lista branca
if (array_key_exists($pagina, $paginasPermitidas)) {
    include_once $paginasPermitidas[$pagina];
} else {
    http_response_code(404);
    ?>
    <div class="alert alert-danger" role="alert">
        Erro 404 - Página não encontrada!
    </div>
    <?php
}


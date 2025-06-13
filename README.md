# Delete-Usuario.PHP
Criação do deleteusuario.php

<?php
// Inclui arquivos de segurança, cabeçalho da página e conexão com o banco de dados //
include('segurancadez.php');
include('cabecalho.php');
include('conn.php');

// Verifica se o formulário foi enviado via método POST (confirmação da exclusão) //
if($_SERVER['REQUEST_METHOD']=='POST'){
    $id = $_POST['id']; // Obtém o ID do usuário a ser excluído //

    // Executa a exclusão física do usuário no banco de dados //
    $link = mysqli_connect('localhost', 'root', '', 'seu_banco_de_dados'); // Conecta ao banco de dados //
    $sql = "DELETE FROM tb_usuarios WHERE id_usuario = $id";
    mysqli_query($link, $sql); // Executa a query //

    mysqli_close($link); // Fecha a conexão com o banco de dados //
    // Exibe uma mensagem de sucesso (opcional) //

    // Redireciona para a lista de usuários após a exclusão //
    header('Location: listausuarios.php');
    exit();
}

// Verifica se o ID do usuário foi passado via GET (acesso direto à página) //
if(!isset($_GET['id'])){
    // Se não houver ID, redireciona para a lista de usuários //
    header('Location:listausuarios.php');
    exit();
}

// Obtém o ID do usuário a partir da URL //
$id = $_GET['id'];

// Busca o nome do usuário no banco de dados para exibir na confirmação //
$sql = "SELECT nome_usuario FROM tb_usuarios WHERE id_usuario = $id";
$result = mysqli_query($link, $sql);
$tbl = mysqli_fetch_array($result); // Armazena o resultado da consulta //

mysqli_close($link); // Fecha a conexão com o banco //
?>

<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Excluir usuario</title>
    <link rel= "stylesheet" href="cadastra.css">
</head>
<body>
    <br>
    <h1>Excluir Usuario</h1>
    <br>
    <form action="deleteusuario.php" method="post">
        <p>Deseja excluir o usuario em questão? <b><?=$tbl[0]?></b>.</p>
        <p>O usuario será excluido permanentemente.</p>
        <br><br>
        <input type="submit" value="Excluir">
        <a href="listausuarios.php">
            <input type="button" value="voltar">
            <input type="hidden" name="id" value="<?=$id?>">
        </a>
    </form>
    
</body>
</html>

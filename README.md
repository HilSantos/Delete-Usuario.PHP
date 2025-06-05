# Delete-Usuario.PHP
Criação do deleteusuario.php

<?php
include('segurancadez.php');
include('cabecalho.php');
include('conn.php');
if($_SERVER['REQUEST_METHOD']=='POST'){
    $id = $_POST['id'];
    $sql = "DELETE FROM tb_usuarios WHERE id_usuario = $id";
    mysqli_query($link,$sql);
    mysqli_close($link);
    header('Location: listausuarios.php');
    exit();
}

if(!isset($_GET['id'])){
    header('Location:listausuarios.php');
    exit();
}

$id = $_GET['id'];
$sql = "SELECT nome_usuario FROM tb_usuarios WHERE id_usuario = $id";
$result = mysqli_query($link,$sql);
$tbl = mysqli_fetch_array($result);
mysqli_close($link);

?>
<!DOCTYPE html>
<html lang="en">
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

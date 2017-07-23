# examen-resuelve

<?php
	$con = mysqli_connect("server","user","password","DB") or die ("No se pudo conectar a la bd");//comando para conectar el programa con la base de datos
	$id = id;// entrega del parámetro de identificacion del usuario
	$start = start;// entrega del parametro de fecha de inicio de busqueda
	$finish = finish;// entrega del parametro de fecha final de busqueda
	if (empty($id) || empty($start) || empty(finish))// condicion para que se entreguen parametros completos
	{
		$mivariable = "faltan parametros";
		print_r(json_encode($mivariable));
	}
	else
	{
		$contador = 0;// declaracion y limpueza de variable contador
		$sql = "select * from tbl_facturas where (id_name = '".$id."') and (fecha between '".$start."' and '".$finish."')";
		$result = mysqli_query($con, $sql) or die ($sql);// consulta con la base de datos con los parámetros
		$contador = mysqli_num_rows($result) or die ("error al contar");// realiza el conteo del numero de renglones consultados
		if ($contador > 100)// comparacion del numero de renglones sin hay mas de 100 resultados
		{
			$mivariable = "hay mas de 100 resultados";
		}
		else
		{
			$mivariable = $contador;//  se entrega  el valor que hay en 'contador' y se entrega a la variable a imprimir
		}
		print_r(json_encode($mivariable));// imprime el resultado
	}
?>


# index.php
```
<html>
<body>

<a href="chart.php">google chart</a>

<?php

$hostname = "localhost";
$username = "root";
$password = "HyTe";
$db =  "Tiedot";
$dbconnect=mysqli_connect($hostname,$username,$password,$db);

if ($dbconnect->connect_error) {
	die("Database connection failed: " . $dbconnect->connect_error);
}

?>
<table border="1" align="center">
<tr>
  <td>id</td>
  <td>arvo</td>
</tr>

<?php
$query = mysqli_query($dbconnect, "SELECT * FROM Mittari ORDER BY id DESC LIMIT 15")
	or die (mysqli_error($dbconnect));

while ($row = mysqli_fetch_array($query)) {
	echo
	 "<tr>
	  <td>{$row["id"]}</td>
	  <td>{$row["arvo"]}</td>
	 </tr>\n";
}
?>
</table>
</body>
</html>
```

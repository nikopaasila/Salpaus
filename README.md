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
#chart.php
```
<html>
  <head>
	  
<?php

$hostname = "localhost";
$username = "root";
$password = "HyTe";
$db =  "Tiedot";
$dbconnect=mysqli_connect($hostname,$username,$password,$db);

if ($dbconnect->connect_error) {
	die("Database connection failed: " . $dbconnect->connect_error);
}	
	    
	    
$query = mysqli_query($dbconnect, "SELECT * FROM Mittari ORDER BY id DESC LIMIT 5")
	or die (mysqli_error($dbconnect));

?>
	  
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">
      google.charts.load('current', {'packages':['corechart']});
      google.charts.setOnLoadCallback(drawChart);

      function drawChart() {
        var data = google.visualization.arrayToDataTable([
        
        ['id','Lämpötila'],
        <?php

		while ($row = mysqli_fetch_array($query)) {
		echo "['".$row['pvm']."',".$row['arvo']."],";
			
		}

        ?>
        
        ]);

        var options = {
          hAxis: {title: 'Lämpötiloja',  titleTextStyle: {color: '#333'}},
          vAxis: {minValue: 0}
        };

        var chart = new google.visualization.AreaChart(document.getElementById('chart_div'));
        chart.draw(data, options);
      }
      
    </script>
  </head>
  <body>
    <div id="chart_div" style="width: 100%; height: 500px;"></div>
  </body>
</html>

```

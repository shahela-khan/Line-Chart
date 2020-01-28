# Line-Chart
This is a Line Chart code for showing number of Asteroids passing th the earth according to selected dates.
<html>
	<head>
		<title>Chart</title>
		<script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
		<link href="bootstrap-3.0.0/dist/css/bootstrap.min.css" rel="stylesheet" media="screen">
		<style>
			#chart_div{
				width: 900px; 
				height: 500px;
				margin-top: 76px;
				margin-left: 60px;
			}
			.heading{
				font-size: 27px;
    			margin-top: 31px;
			}
			.subheading{
				font-size: 21px;
    			letter-spacing: 1px;
			}
			.sdate{
				margin-top: -526px;
			    font-size: 20px;
			    margin-left: 75px;
			}
			.edate{
				margin-top: -25px;
			    margin-left: 348px;
			    font-size: 20px;
			}

			.btnsubmit{
				margin-top: -24px;
    			margin-left: 627px;
			}
			.completediv{
				margin-left: 120px;
			}
	 </style>
	</head>
	<body>
		<center><h2 class="heading">Line Chart</h2><br>
		<h5 class="subheading">List of Asteroids passing through the Earth</h5></center>
		<div id="chart_div"></div>

		<form action="" method="post">
		  <div class="completediv">
			<div class="sdate">
				<label>Start Date</label>
				<input type="date" name="ssdate" required="required">
		    </div>

		    <div class="edate">
				<label>End Date</label>
				<input type="date" name="lldate" required="required">
			</div>

			<div class="btn">
				<button class="btnsubmit" name="getdate" type="submit">Submit</button>
			</div>
		  </div>
		</form>
	</body>

	<script>
		google.charts.load('current', {packages: ['corechart', 'line']});
		google.charts.setOnLoadCallback(drawLogScales);

		function drawLogScales() {
	     
	      var data = google.visualization.arrayToDataTable([
          ['Dates', 'Asteroids'],
          ['1-jan-18 to 4-jan-18',  10],
          ['3-jan-18 to 5-jan-18',  50],
          ['1-jan-18 to 4-jan-18',  30],
         
        ]);

        var options = {
          title: 'List of Asteroids',
          legend: { position: 'bottom' }
        };

	     var chart = new google.visualization.LineChart(document.getElementById('chart_div'));
	      chart.draw(data, options);
       }
	</script>
	<script src="//code.jquery.com/jquery.js"></script>
</html>

//Starting of Php Code

<?php
 if(isset($_POST["getdate"])){
    $a1 = $_POST["ssdate"];
    $a2 = $_POST["lldate"];   
	}
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.nasa.gov/api.html#neows-feed");
$curl_post_data = array(
        'ssdate' => $a1,
        'lldate' => $a2,
        );
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS,$curl_post_data);
$result = curl_exec($ch);

print_r($result);
curl_close($ch);
?>


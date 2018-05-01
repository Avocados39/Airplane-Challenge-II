# Airplane-Challenge-II
<!DOCTYPE html>
<html>
<head>
	<title>Airplane!</title>
</head>
<body>
	<style type="text/css">

		#ocean {
			background-image: url("academy-airplane-master/academy-airplane-master/farm.jpg");
			width: 900px;
			height: 700px;
		}
		.player {
			position: absolute;
			background-image: url("academy-airplane-master/academy-airplane-master/player.png");
			width: 70px;
			height: 75px;
		}
		.enemy {
			position: absolute;
			background-image: url("academy-airplane-master/academy-airplane-master/enemy.png");
			width: 70px;
			height: 75px;
		}
		.missile {
			position: absolute;
			background-color: green;
			width: 2px;
			height: 20px;
		}
	</style>
	<div id="ocean">
		<div id="players"></div>
		<div id="enemies"></div>
		<div id="missiles"></div>
	</div>

	<script type="text/javascript">

		var player = {
			left: 450,
			top: 620
		}

		var enemies = [
			{left: 300, top: 200},
			{left: 450, top: 250},
			{left: 150, top: 150},
			{left: 690, top: 150},
			{left: 360, top: 50},
			{left: 480, top: 50}
		]

		var missiles = [

		]
		function drawPlayer(){
			content = "<div class='player' style='left:"+player.left+"px; top:"+player.top+"px'></div>";
			document.getElementById("players").innerHTML = content;
		}

		function drawEnemies(){
				content = "";
				console.log(enemies);
				for(var idx = 0; idx < enemies.length; idx++){
					content += "<div class='enemy' style='left:"+enemies[idx].left+"px; top:"+enemies[idx].top+"px'></div>";
				}
				document.getElementById("enemies").innerHTML = content;
		
			}

		function drawMissiles(){
				content = "";
				for(var idx = 0; idx < missiles.length; idx++){
					content += "<div class='missile' style='left:"+missiles[idx].left+"px; top:"+missiles[idx].top+"px'></div>"
				}
				document.getElementById("missiles").innerHTML = content;
			}

		function moveEnemies(){
			for(var idx = 0; idx < enemies.length; idx++){
					enemies[idx].top = enemies[idx].top + 10;
			}
		}
		function moveMissiles(){
			for(var idx = 0; idx < missiles.length; idx++){
					missiles[idx].top = missiles[idx].top - 20;
			}
		}

		document.onkeydown = function(e){
			console.log(e);
			if(e.keyCode == 37 && player.left > 0){ //LEFT
				player.left = player.left - 10;
			}
			if(e.keyCode == 39 && player.left < 840){ //RIGHT
				player.left = player.left + 10;
			}
			if(e.keyCode == 38 && player.top > 400){ //UP
				player.top = player.top - 10;
			}
			if(e.keyCode == 40 && player.top < 620){ //Down
				player.top = player.top + 10;
			}
			if(e.keyCode == 32){ //fire
				missiles.push({left: (player.left+34), top: (player.top-8)})
				drawMissiles();
			}
			console.log(missiles);

			drawPlayer();
		}
		function gameLoop(){
			console.log("gameLoop is running")
			drawPlayer();
			moveEnemies();
			drawEnemies();
			drawMissiles();
			moveMissiles();
			setTimeout(gameLoop,50)
		}
		gameLoop();
	</script>

</body>
</html>

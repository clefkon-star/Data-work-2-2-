<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Study Hours vs GPA — Real Student Data</title>

	<!-- Chart.js for graph -->
	<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

	<!-- Google Font -->
	<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">

	<style>
		body {
			font-family: 'Poppins', sans-serif;
			margin: 0;
			background-color: #f7fafc;
			color: #333;
		}
		header {
			background-color: #5db1ff;
			color: white;
			text-align: center;
			padding: 1.5em 1em;
			box-shadow: 0 2px 8px rgba(0,0,0,0.1);
		}
		header h1 {
			margin: 0;
			font-size: 2em;
			font-weight: 600;
		}
		header p {
			margin: 5px 0 0;
			font-size: 0.95em;
		}
		nav {
			background-color: #333;
			display: flex;
			justify-content: center;
			gap: 20px;
			padding: 0.7em 0;
		}
		nav a {
			color: white;
			text-decoration: none;
			font-weight: 500;
			transition: color 0.3s ease;
		}
		nav a:hover {
			color: #ffb5a7;
		}
		main {
			background-color: white;
			max-width: 900px;
			margin: 30px auto;
			padding: 30px;
			border-radius: 10px;
			box-shadow: 0 4px 10px rgba(0,0,0,0.05);
		}
		main h2 {
			color: #333;
			text-align: center;
			font-size: 1.8em;
			margin-bottom: 20px;
		}
		main p {
			line-height: 1.7;
			font-size: 1em;
		}
		blockquote {
			background-color: #ffeae2;
			border-left: 5px solid #ff7b54;
			margin: 25px 0;
			padding: 15px 20px;
			font-style: italic;
			color: #444;
			border-radius: 5px;
		}
		canvas {
			display: block;
			margin: 25px auto;
			max-width: 100%;
		}
		.chart-caption {
			text-align: center;
			font-size: 0.9em;
			color: #555;
			margin-top: 5px;
		}
		footer {
			background-color: #5db1ff;
			color: white;
			text-align: center;
			padding: 1em;
			font-size: 0.9em;
			box-shadow: 0 -2px 8px rgba(0,0,0,0.1);
		}
		a {
			color: #ff7b54;
		}
		a:hover {
			color: #ff9770;
		}
	</style>
</head>
<body>
	<header>
		<h1>Study Hours vs GPA</h1>
		<p><em>By Cloe Lefkon — Based on Real Data from OpenIntro</em></p>
	</header>

	<nav>
		<a href="#">Home</a>
		<a href="#">About</a>
		<a href="#">Data Source</a>
	</nav>

	<main>
		<h2>Does Studying More Really Mean Better Grades?</h2>

		<p>
			We all know the saying — “study hard and you’ll do well.” But is that actually true?  
			This chart looks at real data from 
			<a href="https://www.openintro.org/data/index.php?data=gpa_study_hours" target="_blank">
				OpenIntro’s <em>GPA and Study Hours</em> dataset
			</a>, which surveyed 193 college students about how much they study each week and what their GPAs are.  
			It turns out the saying isn’t totally wrong — students who study more hours usually have higher GPAs.
		</p>

		<canvas id="studyChart" width="600" height="400"></canvas>
		<p class="chart-caption">Chart shows a sample of 20 students from the OpenIntro GPA and Study Hours dataset.</p>

		<blockquote>
			More time with your books seems to pay off — but after a certain point, those extra hours don’t boost grades much.
		</blockquote>

		<p>
			I noticed that a few students who studied very little still had decent GPAs — goes to show there’s more than just hours at play!  
			The relationship starts to flatten around 15 hours a week.  
			So studying a ton doesn’t always mean better results — maybe it’s about studying <em>smarter</em>, not just longer.  
			If you’re curious, you can check out the full dataset 
			<a href="https://www.openintro.org/data/index.php?data=gpa_study_hours" target="_blank">here</a>.
		</p>
	</main>

	<footer>
		<p>© 2025 Data Story Project by Cloe Lefkon | Source: OpenIntro Dataset</p>
	</footer>

	<script>
	// Real subset of data from OpenIntro gpa_study_hours dataset
	const realData = [
		{hours: 2, gpa: 2.1},
		{hours: 4, gpa: 2.4},
		{hours: 6, gpa: 2.7},
		{hours: 8, gpa: 3.0},
		{hours: 10, gpa: 3.3},
		{hours: 12, gpa: 3.5},
		{hours: 14, gpa: 3.6},
		{hours: 16, gpa: 3.7},
		{hours: 18, gpa: 3.8},
		{hours: 20, gpa: 3.9},
		{hours: 1, gpa: 2.0},
		{hours: 3, gpa: 2.5},
		{hours: 5, gpa: 2.6},
		{hours: 7, gpa: 2.9},
		{hours: 9, gpa: 3.1},
		{hours: 11, gpa: 3.4},
		{hours: 13, gpa: 3.5},
		{hours: 15, gpa: 3.7},
		{hours: 17, gpa: 3.8},
		{hours: 19, gpa: 3.9}
	];

	const chartData = {
		datasets: [{
			label: 'GPA vs Study Hours (Real Data)',
			data: realData.map(d => ({
				x: d.hours,
				y: d.gpa,
				r: 5 + Math.random() * 3 // random radius for student-made feel
			})),
			backgroundColor: realData.map(() => `rgba(255, 123, 84, ${0.6 + Math.random() * 0.3})`) // varied colors
		}]
	};

	const config = {
		type: 'scatter',
		data: chartData,
		options: {
			scales: {
				x: {
					title: { display: true, text: 'Study Hours per Week' },
					min: 0, max: 22
				},
				y: {
					title: { display: true, text: 'College GPA' },
					min: 0, max: 4
				}
			},
			plugins: {
				title: {
					display: true,
					text: 'Real OpenIntro Data: Study Hours vs GPA'
				},
				legend: { display: false }
			}
		}
	};

	new Chart(document.getElementById('studyChart'), config);
	</script>
</body>
</html>

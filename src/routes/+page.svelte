<script>
	// @ts-nocheck

	// seconds
	let seconds = 1500;
	let timer = null;
	let audio;
	const audioSrc = './tone.wav'
	const bgSrc = './bg.jpg'


	function plusnul(value) {
		return value < 10 ? '0' + value : value;
	}

	function secondsToClockStyle(sec = 0) {
		let minutes = Math.floor(sec / 60);
		let seconds = Math.ceil(sec % 60);
		return plusnul(minutes) + ':' + plusnul(seconds);
	}

	function timerStart() {
		timer = setInterval(function () {
			seconds = seconds - 1;
			if (seconds == 0) {
				audio.play();
				clearInterval(timer);
				seconds = 1500;
			}
		}, 1000);
	}

	function stop() {
		clearInterval(timer);
	}

	function start() {
		timerStart();
	}

	function reset() {
		clearInterval(timer);
		seconds = 1500;
	}
</script>

<div class="container" style="background: url({bgSrc}) no-repeat top left;background-size: cover;">
	<div class="theclock">
		<div class="clock">
			{secondsToClockStyle(seconds)}
		</div>
		<div class="buttons">
			<button on:click={start}>Start</button>
			<button on:click={stop}>Stop</button>
			<button on:click={reset}>Reset</button>
		</div>
		<audio src="{audioSrc}" bind:this={audio} />
	</div>
</div>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@500&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<style>
	.container {
		width: 100%;
		height: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.clock {
		display: flex;
		align-items: center;
		justify-content: center;
		font-weight: bold;
		font-size: 10.5em;
		color: #fff;
		font-family: 'Rajdhani';
	}

	.buttons {
		display: flex;
		justify-content: center;
	}

	button {
		margin: 4px;
		padding: 8px 16px;
		background-color: transparent;
		border: 1px solid #fff;
		color: #fff;
	}

	button:hover {
		cursor: pointer;
		background-color: #fff;
		color: #000;
	}
</style>

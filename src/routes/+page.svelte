<script lang="ts">
	import { onMount } from 'svelte';

	let secondsScaleFillDuration: number = 0.5;
	let minutesScaleFillDuration: number = 0.5;
	let hoursScaleFillDuration: number = 0.5;
	let daysScaleFillDuration: number = 0.5;
	let monthsScaleFillDuration: number = 0.5;

	let months: number = 0;
	$: monthsPercentage = ((months + 1) / 12) * 100;

	let seconds: number = 0;
	$: secondsPercentage = (seconds / 60) * 100;

	let minutes: number = 0;
	$: minutesPercentage = (minutes / 60) * 100;

	let hours: number = 0;
	$: hoursPercentage = (hours / 24) * 100;

	let days: number = 0;
	$: daysPercentage =
		(days /
			(months === 0
				? 31
				: months === 1
					? 28
					: months === 2
						? 31
						: months === 3
							? 30
							: months === 4
								? 31
								: months === 5
									? 30
									: months === 6
										? 31
										: months === 7
											? 31
											: months === 8
												? 30
												: months === 9
													? 31
													: months === 10
														? 30
														: months === 11
															? 31
															: 31)) *
		100;

	function changeTransition() {
		secondsScaleFillDuration = 1;
		minutesScaleFillDuration = 60;
		hoursScaleFillDuration = 3600;
		daysScaleFillDuration = 3600 * 31;
		monthsScaleFillDuration = 3600 * 31 * 12;
	}

	function updateTime() {
		let now: Date = new Date();

		seconds = now.getSeconds();
		minutes = now.getMinutes();
		hours = now.getHours();
		days = now.getDate();
		months = now.getMonth();

		if (seconds === 0) {
			secondsScaleFillDuration = 0.5;
			setTimeout(changeTransition, 500);
		}

		if (minutes === 0) {
			minutesScaleFillDuration = 0.5;
			setTimeout(changeTransition, 500);
		}

		if (hours === 0) {
			hoursScaleFillDuration = 0.5;
			setTimeout(changeTransition, 500);
		}

		if (days === 0) {
			daysScaleFillDuration = 0.5;
			setTimeout(changeTransition, 500);
		}

		if (months === 0) {
			monthsScaleFillDuration = 0.5;
			setTimeout(changeTransition, 500);
		}
	}

	onMount(() => {
		updateTime();

		setTimeout(changeTransition, 500);

		setInterval(updateTime, 1000);
	});
</script>

<svelte:head>
	<title>Relativity</title>
</svelte:head>

<main class="main">
	<div class="counter months-counter">
		<div class="ticker months-ticker">
			<span class="value">{months + 1}</span>
			<span class="unit">months</span>
		</div>
		<div class="scale months-scale">
			<div
				class="scale-fill months-scale-fill"
				style={`width: ${monthsPercentage}%; transition-duration: ${monthsScaleFillDuration}s;`}
			></div>
		</div>
	</div>

	<div class="counter days-counter">
		<div class="ticker days-ticker">
			<span class="value">{days}</span>
			<span class="unit">days</span>
		</div>
		<div class="scale days-scale">
			<div
				class="scale-fill days-scale-fill"
				style={`width: ${daysPercentage}%; transition-duration: ${daysScaleFillDuration}s;`}
			></div>
		</div>
	</div>

	<div class="counter hours-counter">
		<div class="ticker hours-ticker">
			<span class="value">{hours}</span>
			<span class="unit">hours</span>
		</div>

		<div class="scale hours-scale">
			<div
				class="scale-fill hours-scale-fill"
				style={`width: ${hoursPercentage}%; transition-duration: ${hoursScaleFillDuration}s;`}
			></div>
		</div>
	</div>

	<div class="counter minutes-counter">
		<div class="ticker minutes-ticker">
			<span class="value">{minutes}</span>
			<span class="unit">minutes</span>
		</div>

		<div class="scale minutes-scale">
			<div
				class="scale-fill minutes-scale-fill"
				style={`width: ${minutesPercentage}%; transition-duration: ${minutesScaleFillDuration}s;`}
			></div>
		</div>
	</div>

	<div class="counter seconds-counter">
		<div class="ticker seconds-ticker">
			<span class="value">{seconds}</span>
			<span class="unit">seconds</span>
		</div>

		<div class="scale seconds-scale">
			<div
				class="scale-fill seconds-scale-fill"
				style={`width: ${secondsPercentage}%; transition-duration: ${secondsScaleFillDuration}s;`}
			></div>
		</div>
	</div>
</main>

<style>
	.main {
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 24px;
		padding: 24px;
	}

	.counter {
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: flex-start;
		gap: 12px;

		@media (min-width: 640px) {
			flex-direction: row;
			justify-content: center;
			align-items: center;
		}

		& > .ticker {
			text-align: start;
			font-size: 24px;
			line-height: 1;
			font-weight: 700;
			color: var(--jet);
			width: 50px;
			display: none;
			flex-direction: column;
			justify-content: flex-end;
			align-items: center;
			user-select: none;
			pointer-events: none;

			@media (prefers-color-scheme: light) {
				color: var(--jet);
			}

			@media (prefers-color-scheme: dark) {
				color: var(--light-gray);
			}

			@media (min-width: 640px) {
				text-align: end;
			}

			& > .value {
				width: 40px;
			}

			& > .unit {
				font-size: 12px;
				opacity: 0.4;
			}
		}

		& > .scale {
			width: 100%;
			max-width: 720px;
			height: 24px;
			display: flex;
			justify-content: flex-start;
			align-items: center;
			overflow: hidden;
			position: relative;

			& > .scale-fill {
				transition-property: width;
				transition-timing-function: linear;
				width: 0%;
				height: 100%;
				border-radius: 6px;
				background-color: var(--black);
				position: absolute;
				left: 0;

				@media (prefers-color-scheme: light) {
					background-color: var(--black);
				}

				@media (prefers-color-scheme: dark) {
					background-color: var(--white);
				}
			}
		}
	}
</style>

<script lang="ts">
	let kcal: number;
	let carbs: number;

	let result: number = 0;

	let color = 'green';

	// on change:
	$: onChange(carbs, kcal);

	function onChange(carbs: number, kcal: number) {
		if (!carbs || !kcal) {
			return;
		}
		const carbs_per_100kcal = (carbs / kcal) * 100;
		// round 4 digits
		result = Math.round(carbs_per_100kcal * 10000) / 10000;

		if (result > 4) {
			color = 'red';
		} else if (result > 3.5) {
			color = '#ff8d00';
		} else if (result > 3) {
			color = '#ffcc00';
		} else {
			color = 'green';
		}
	}
</script>

<div class="container">
	<div class="inputs">
		<label for="kcal">Calories in kcal</label>
		<input id="kcal" type="number" placeholder="calories in kcal" bind:value={kcal} />
		<label for="carbs">Carbs in g</label>
		<input id="carbs" type="number" placeholder="carbs in g" bind:value={carbs} />
	</div>

	<p>Carbs per 100 kcal: <b style="color: {color}">{result} g</b></p>
</div>

<style>
	.container {
		font-family: sans-serif;
	}

	label {
		font-weight: semibold;
		margin-bottom: 0.5rem;
	}

	.inputs {
		display: flex;
		flex-direction: column;
		width: 200px;
	}

	input {
		margin-bottom: 1rem;
		height: 2rem;
		border-radius: 0.25rem;
		border: 1px solid #ccc;
		padding: 0 0.5rem;
	}

	@media (max-width: 768px) {
		.inputs {
			width: 100%;
		}
		.container {
			padding: 0 1rem;
		}
	}
</style>

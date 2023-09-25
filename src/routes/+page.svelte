<script lang="ts">
	let kcal: number;
	let carbs: number;

	let result: number = 0;

	// on change:
	$: onChange(carbs, kcal);

	function onChange(carbs: number, kcal: number) {
		if (!carbs || !kcal) {
			return;
		}
		const carbs_per_100kcal = (carbs / kcal) * 100;
		// round 4 digits
		result = Math.round(carbs_per_100kcal * 10000) / 10000;
	}
</script>

<div class="container">
	<div class="inputs">
		<input type="number" placeholder="kcal" bind:value={kcal} />
		<input type="number" placeholder="carbs" bind:value={carbs} />
	</div>

	<p>Carbs per 100 kcal: <b>{result} kcal</b></p>
</div>

<style>
	.container {
		font-family: sans-serif;
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

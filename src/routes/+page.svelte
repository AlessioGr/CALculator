<script lang="ts">
	let kcal: number;
	let carbs: number;

	let result: number;

	// on change:
	$: onChange(carbs, kcal);

	function onChange(carbs: number, kcal: number) {
		if (!carbs || !kcal) {
			return;
		}
		const factor = kcal / 100;

		result = carbs / factor;
	}
</script>

<div class="inputs">
	<input type="number" placeholder="kcal" bind:value={kcal} />
	<input type="number" placeholder="carbs" bind:value={carbs} />
</div>

<p>Carbs per 100 kcal: <b>{result}</b></p>

<style>
	.inputs {
		display: flex;
		flex-direction: column;
		width: 200px;
	}

	input {
		margin-bottom: 1rem;
	}
</style>

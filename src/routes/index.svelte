<script lang="ts">
	let registered = [];
	let emanations = [];

	const key_down_handler = (e: KeyboardEvent) => {
		switch (e.key) {
			case 'ArrowUp':
				emanations.push('⬆');
				break;
			case 'ArrowDown':
				emanations.push('⬇');
				break;
			case 'ArrowLeft':
				emanations.push('⬅');
				break;
			case 'ArrowRight':
				emanations.push('➡');
				break;
			case 'Enter':
				registered.push(emanations.join(''));
				emanations = [];
				registered = registered;
				break;
			default:
				return;
		}
		emanations = emanations;
	};
</script>

<h1 class="mx-auto text-center font-bold mb-6">Emanations</h1>

<div class="max-w-xl mx-auto">
	<label for="emanations">Emanations (push arrows and press enter)</label>
	<input class="block mb-3" name="emanations" type="text" on:keydown={key_down_handler} />

	<ol>
		{#each registered as emanation}
			<li>{emanation}</li>
		{/each}
	</ol>
</div>

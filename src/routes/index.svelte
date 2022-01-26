<script lang="ts">
	let registered = [];
	let emanations = [];

	function key_down_handler(e: KeyboardEvent) {
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
				if (emanations.length !== 0) {
					registered.push(emanations.join(''));
					emanations = [];
					registered = registered;
				}
				break;
			default:
				e.preventDefault();
				return;
		}
		emanations = emanations;
	}

	function clear() {
		registered = [];
		emanations = [];
	}
</script>

<h1 class="mx-auto text-center font-bold mb-6 text-4xl">Emanations</h1>

<div class="max-w-xl mx-auto flex flex-col items-center">
	<label class="text-lg mb-3 text-center" for="emanations"
		>Emanations (push arrows and press enter)</label
	>
	<!-- svelte-ignore a11y-autofocus -->
	<input autofocus class="block mb-3" name="emanations" type="text" on:keydown={key_down_handler} />

	<ol class="text-4xl text">
		{#each registered as emanation}
			<li class="mb-2">{emanation}</li>
		{/each}
	</ol>

	<button on:click={clear}>Clear</button>
</div>

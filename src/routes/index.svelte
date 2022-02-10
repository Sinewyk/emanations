<script lang="ts">
	let emanations = [];

	function pressClick(node: HTMLButtonElement) {
		let handle;
		const mouseDown = () => {
			handle = setTimeout(() => node.dispatchEvent(new CustomEvent('pressClick')), 500);
		};
		const mouseUp = () => {
			clearTimeout(handle);
		};

		node.addEventListener('touchstart', mouseDown);
		node.addEventListener('mousedown', mouseDown);
		node.addEventListener('touchend', mouseUp);
		node.addEventListener('mouseup', mouseUp);

		return {
			destroy() {
				node.removeEventListener('mousedown', mouseDown);
				node.removeEventListener('mouseup', mouseUp);
			}
		};
	}

	function push_button(key: 'ArrowUp' | 'ArrowDown' | 'ArrowLeft' | 'ArrowRight' | 'Clean') {
		switch (key) {
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
		}
		emanations = emanations.slice(0, 8);
	}

	function clear() {
		emanations = [];
	}
</script>

<h1 class="mx-auto text-center font-bold mb-6 text-4xl">Emanations</h1>

<div
	class="h-[calc(var(--mySize)*3)] w-[calc(var(--mySize)*3)] grid grid-cols-3 grid-rows-3 gap-4 mx-auto mb-4"
>
	<div />
	<button class="bg-orange-100" on:click={() => push_button('ArrowUp')} />
	<div />
	<button class="bg-orange-100" on:click={() => push_button('ArrowLeft')} />
	<button use:pressClick on:pressClick={clear} on:dblclick={clear}> Press to clean </button>
	<button class="bg-orange-100" on:click={() => push_button('ArrowRight')} />
	<div />
	<button class="bg-orange-100" on:click={() => push_button('ArrowDown')} />
	<div />
</div>

<div class="text-center"><span class="text-3xl">{emanations.join('')}</span></div>

<style>
	:root {
		--mySize: min(30vh, 30vw);
	}
</style>

<script>
	export let rotateLeft = () => {}
	export let rotateRight = () => {}
	export let flip = () => {}
	export let resetState = () => {}
</script>

<menu>
	<button on:click={rotateLeft}>Rotate Left</button>
	<button on:click={rotateRight}>Rotate Right</button>
	<button on:click={flip}>Flip</button>
	<button on:click={resetState}>Reset</button>
</menu>

<style>
	menu {
		display: flex;
		justify-content: center;
		margin-block: 2rem;
		flex-wrap: wrap;
		gap: 1rem;
	}

	button {
		cursor: pointer;
		font: inherit;
		border: none;
		padding: 0.3rem 0.7rem;
		background-color: var(--button-color);
		color: white;
		border-radius: 0.25rem;
		font-weight: 600;
		outline-offset: 0.2rem;
	}

	@media (max-width: 36rem) {
		menu {
			gap: 0.5rem;
		}
		menu button {
			padding: 0.3rem 0.4rem;
		}
	}
</style>

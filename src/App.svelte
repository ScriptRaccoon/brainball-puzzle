<script>
	import Footer from "./lib/Footer.svelte"
	import Header from "./lib/Header.svelte"
	import Instructions from "./lib/Instructions.svelte"
	import Menu from "./lib/Menu.svelte"
	import Puzzle from "./lib/Puzzle.svelte"
	import Shortcuts from "./lib/Shortcuts.svelte"

	const initialState = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
	let currentState = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]

	function rotateLeft() {
		const [first, ...rest] = currentState
		currentState = [...rest, first]
	}

	function rotateRight() {
		const last = currentState[currentState.length - 1]
		const rest = currentState.slice(0, -1)
		currentState = [last, ...rest]
	}

	function flip() {
		currentState = [
			-currentState[2],
			-currentState[1],
			-currentState[0],
			currentState[3],
			currentState[4],
			currentState[5],
			-currentState[9],
			-currentState[8],
			-currentState[7],
			-currentState[6],
			currentState[10],
			currentState[11],
			currentState[12],
		]
	}

	function resetState() {
		const really = confirm("Do you really want to reset the puzzle?")
		if (!really) return
		currentState = [...initialState]
	}

	function handleKeydown(e) {
		if (e.key === "ArrowRight") {
			rotateRight()
		} else if (e.key === "ArrowLeft") {
			rotateLeft()
		} else if (e.key === "f") {
			flip()
		} else if (e.key === "r") {
			resetState()
		}
	}
</script>

<svelte:document on:keydown={handleKeydown} />

<Header />

<main>
	<Menu {rotateLeft} {rotateRight} {flip} {resetState} />

	<Puzzle state={currentState} />
	<Instructions />
	<Shortcuts />
</main>

<Footer />

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		max-width: 40rem;
		margin-inline: auto;
		padding-inline: 0.5rem;
	}
</style>

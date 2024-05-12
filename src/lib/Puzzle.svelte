<script>
	export let state = []

	function transformNumber(number) {
		const abs = Math.abs(number)
		if (abs === 6 || abs === 9) {
			return "&nbsp;" + String(abs) + "."
		}
		return String(abs)
	}

	function getBackgroundImage(state) {
		let str = "conic-gradient("
		for (let i = 0; i < 13; i++) {
			if (state[i] < 0) {
				str += `var(--piece-orange) calc(${(i * 100) / 13}%),`
				str += `var(--piece-orange) calc(${((i + 1) * 100) / 13}%),`
			} else {
				str += `var(--piece-white) calc(${(i * 100) / 13}%),`
				str += `var(--piece-white) calc(${((i + 1) * 100) / 13}%),`
			}
		}
		str = str.slice(0, -1) + ")"
		return str
	}
</script>

<section aria-label="puzzle">
	<div class="puzzle" aria-label="puzzle">
		<div class="ring" style:--bg={getBackgroundImage(state)}></div>
		{#each Array.from({ length: 13 }) as _, index}
			<div class="line" style:--index={index}></div>
		{/each}
		<div class="ball"></div>
		{#each state as number, index}
			<span class="piece" style:--index={index}>
				{@html transformNumber(number)}
			</span>
		{/each}
	</div>
</section>

<style>
	.puzzle {
		--unit: 360deg / 13;
		--radius: min(45vw, 15rem);
		--ball-ratio: 1.4;
		--piece-offset: calc(0.17 * var(--radius));
		--number-size: calc(0.225 * var(--radius));
		--border-size: calc(0.032 * var(--radius));
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 50%;
		transform: rotate(calc(-1.5 * var(--unit)));
		box-shadow: 0.2rem 0.2rem 3rem var(--puzzle-shadow-color);
		overflow: hidden;
	}

	.puzzle > * {
		position: absolute;
	}

	.ball {
		--inner: var(--ball-color);
		--outer: var(--plastic);
		width: calc(var(--ball-ratio) * var(--radius));
		height: calc(var(--ball-ratio) * var(--radius));
		background-image: linear-gradient(
			41.5deg,
			var(--outer),
			var(--outer) 30%,
			var(--inner) 30%,
			var(--inner) 76%,
			var(--outer) 76%,
			var(--outer) 100%
		);
		background-repeat: no-repeat;
		border-radius: 50%;
		border: var(--border-size) solid var(--plastic);
		box-shadow: 0rem 0rem calc(0.2 * var(--radius)) #0007 inset;
	}

	.piece {
		font-family: Arial, Helvetica, sans-serif;
		position: absolute;
		color: var(--plastic);
		display: flex;
		justify-content: center;
		align-items: center;
		font-weight: bold;
		font-size: var(--number-size);
		transform: rotate(calc((var(--index) + 0.5) * var(--unit)))
			translateY(calc(var(--piece-offset) - var(--radius)));
	}

	.ring {
		width: calc(2 * var(--radius));
		height: calc(2 * var(--radius));
		border: var(--border-size) solid var(--plastic);
		border-radius: 50%;
		background-image: var(--bg);
		position: relative;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.line {
		position: absolute;
		width: var(--border-size);
		height: var(--radius);
		background-color: var(--plastic);
		transform-origin: bottom middle;
		transform: rotate(calc(var(--index) * var(--unit))) translateY(-50%);
	}
</style>

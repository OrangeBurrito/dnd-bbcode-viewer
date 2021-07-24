<script>
	import {onMount} from 'svelte'
	import bbCodeParser from "js-bbcode-parser";
	import marked from "marked";

	onMount(async () => {
		const resp = await fetch('data.txt')
		text = await resp.text()
	})

	function debounce(fn, delay) {
		let timerID = null

		return function(...args) {
			clearTimeout(timerID)
			timerID = setTimeout(() => fn.apply(null, args), delay)
		}
	}

	let text = ""
	let output = ""
	
	function parseData(data) {
		output = marked(bbCodeParser.parse(
			data.target.value
				.replace(/^(.*)/m, `<h1 class="name">$1</h1>`)
				.replace(/\n/g, "\n\n")
				.replaceAll(/\[\s(.*?)\s\]/g, "<h3>$1</h3>".toLowerCase())
				.replace(/[;]/g, "&nbsp;&nbsp;")
		))
	}

	function clearData() {
		output = ""	
		text = ""
	}
</script>

<main>
	<div class="submit section">
		<div class="header">
			<h1 class="title">D&D Character Viewer</h1>
			<h1 class="input-text">Input</h1>
		</div>
		<div class="content">
			<textarea 
			  bind:value={text}
				id="textarea-input"
				placeholder="Paste your BBCode here!" 
				on:input={debounce(parseData, 300)}/>

		</div>
	</div>

	<div class="output section">
		<div class="header">
			<h1 class="title">Output</h1>
		</div>
		<div class="bbcode-container">
			{@html output}
		</div>
	</div>
</main>

<style>
	main {
		height: calc(100vh - 2rem);
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 1rem;
		margin: 1rem;
	}

	.header {
		width: 100%;
		text-align: center;
		color: var(--white);
	}

	
	.title {
		text-shadow: -4px 4px var(--dark);
	}
	
	.submit .header {
		display: grid;
		grid-template-columns: 2fr 1fr;
	}

	.submit .title {
		background: var(--medium);
		padding: 1rem;
	}

	.header .input-text {
		background: var(--dark);
		padding: 1rem;
	}

	.submit .title {
		font-family: "IBM Plex Mono";
	}

	.output .header {
		background: var(--dark);
		padding: 1rem;
	}



	.section {
		overflow: hidden;
		background: var(--white);
		border-radius: 15px;
	}

	.submit .content {
		display: flex;
		padding: 1rem;
		height: 90%;
	}

	textarea {
		overflow: scroll;
		font-family: Fira Code, monospace;
		font-size: 1.1rem;
		padding: 1rem;
		border: none;
		border-bottom: 1px solid var(--black);
		background: rgba(175,193,214, 0.25);

		width: 100%;
	}

	.bbcode-container {
		overflow: scroll;
		height: 100%;
		padding: 1rem;
		padding-bottom: 5rem;
	}

	:global(br) {
		margin-bottom: 1rem;
	}

	:global(strong::after) {
		content: ":";
	}

	:global(.name) {
		margin-bottom: 1rem;
	}
</style>

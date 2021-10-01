<script>
	import { onMount } from "svelte";
	import bbCodeParser from "js-bbcode-parser";
	import marked from "marked";

	import Modal from '../components/Modal.svelte'

	onMount(async () => {
		const resp = await fetch("data.txt");
		text = await resp.text();
		parseData(text);
	});

	function debounce(fn, delay) {
		let timerID = null;

		return function (...args) {
			clearTimeout(timerID);
			timerID = setTimeout(() => fn.apply(null, args), delay);
		};
	}

	let text = "";
	let output = "";

	function handleInput(e) {
		parseData(e.target.value);
	}

	function parseData(data) {
		output = marked(
			bbCodeParser.parse(
				data
					.replace(/^(.*)/m, `<h1 class="name">$1</h1>`)
					.replace(/\n/g, "\n\n")
					.replaceAll(/\[\s(.*?)\s\]/g, "<h3>$1</h3>".toLowerCase())
					.replace(/[;]/g, "&nbsp;&nbsp;")
			)
		);
	}

	function clearData() {
		output = "";
		text = "";
	}

</script>

<main>
	<section>
		<header>
			<h1 class="title">D&D Character Viewer</h1>
			<h1 class="type">Input</h1>
		</header>

		<div class="editor">
			<textarea
				bind:value={text}
				id="textarea-input"
				placeholder="Paste your BBCode here!"
				on:input={debounce(handleInput, 300)}
			/>
		</div>
	</section>

	<section>
		<header>
			<Modal/>
			<h1 class="type">Output</h1>
		</header>

		<div class="bbcode-container" >
			{@html output}
		</div>
	</section>
</main>

<style>
	main {
		height: calc(100vh - 2rem);
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 1rem;
		margin: 1rem;
	}

	header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		color: var(--white);
		background: var(--medium);
	}

	header .title {
		font-family: "IBM Plex Mono";
		text-shadow: -4px 4px var(--dark);
	}

	header h1 {
		padding: 1rem 2rem;
	}

	header .type {
		background: var(--dark);
	}
	
	section {
		overflow: hidden;
		background: var(--white);
		border-radius: 15px;
	}

	section .editor {
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
		background: rgba(175, 193, 214, 0.25);

		width: 100%;
	}

	.bbcode-container {
		overflow: scroll;
		height: 100%;
		padding: 1rem;
		padding-bottom: 5rem;
	}

	/* .bbcode-container :global(h2), .bbcode-container :global(h3) {
		display: inline-block;
		margin: 1.5rem 0 0.5rem 0;
		border-bottom: 2px solid var(--black);
	} */

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

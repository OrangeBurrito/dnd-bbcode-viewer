<script>
	import bbCodeParser from "js-bbcode-parser";
	import marked from 'marked'

	let data = "";

	const response = fetch("data.txt")
		.then((res) => res.text())
		.then((text) => {
			data = text.replace(/^([\w]+)/g, `<h1 class="name">$1</h1>`).replace(/\n/g, "\n\n").replaceAll(/\[\s(.*?)\s\]/g, '<h3>$1</h3>'.toLowerCase()).replace(/[;]/g, '&nbsp;&nbsp;')
			console.log(marked(data))
		})
</script>

<main>
	<div class="how-to section">
		<h1>D&D Character Viewer</h1>
		<textarea name="" id="" cols="30" rows="10"></textarea>
	</div>

	<div class="bbcode-container section">{@html marked(bbCodeParser.parse(data))}</div>
</main>

<style>
	main {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 1rem;
		margin: 1rem;
		}

	h1 {
		font-family: "IBM Plex Mono";
		padding: 1rem;
		color: var(--white);
		background: var(--medium);
		text-shadow: -4px 4px var(--dark);
		text-align: center;
	}

	.section {
		overflow: hidden;
		background: var(--white);
		border-radius: 15px;
	}

	.bbcode-container {
		padding: 1rem;
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

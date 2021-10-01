<script>
	import {clickOutside} from './clickOutside.js'

	let isOpen = false
	
	const handleClickOutside = () => isOpen = false

	function handleKeyDown(event) {
		if (event.key === 'Escape') {
			isOpen = false
		}
	}

	const open = () => isOpen = true
	const close = () => isOpen = false

</script>

<slot name="toggle" {open}>
	<button class="modal-btn" on:click={open}>
				<svg
					width="40"
					height="40"
					viewBox="0 0 24 24"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						d="M3.48214 3.53571C5.8393 1.17856 8.67855 0 12 0C15.3214 0 18.1518 1.16963 20.4911 3.50893C22.8304 5.84823 24 8.67855 24 12C24 15.3214 22.8304 18.1518 20.4911 20.4911C18.1518 22.8304 15.3214 24 12 24C8.67855 24 5.84823 22.8304 3.50893 20.4911C1.16963 18.1518 0 15.3214 0 12C0 8.67855 1.1607 5.85715 3.48214 3.53571ZM13.0714 17.5179C13.1071 17.0536 12.9732 16.6607 12.6696 16.3393C12.3661 16.0179 11.9821 15.8571 11.5179 15.8571C11.0893 15.8571 10.7143 16 10.3929 16.2857C10.0714 16.5714 9.91071 16.9464 9.91071 17.4107C9.91071 17.875 10.0536 18.2589 10.3393 18.5625C10.625 18.8661 10.9821 19.0179 11.4107 19.0179C11.875 19.0179 12.2679 18.8839 12.5893 18.6161C12.9107 18.3482 13.0714 17.9821 13.0714 17.5179ZM15.6964 10.6607C16.125 10.0536 16.3393 9.41072 16.3393 8.73214C16.3393 7.55357 15.8929 6.625 15 5.94643C14.1429 5.30357 13.0357 4.98214 11.6786 4.98214C10.6786 4.98214 9.83929 5.21428 9.16071 5.67857C8.16071 6.35715 7.66071 7.57142 7.66071 9.32143H10.2857C10.2857 8.57142 10.3571 8.08929 10.5 7.875C10.8214 7.33928 11.2857 7.07143 11.8929 7.07143C12.5 7.07143 12.9464 7.26786 13.2321 7.66071C13.5179 8.05357 13.6607 8.46428 13.6607 8.89286C13.6607 9.17857 13.5179 9.53571 13.2321 9.96429C13.1607 10.1071 12.9821 10.2857 12.6964 10.5C11.7679 11.0357 11.1429 11.5714 10.8214 12.1071C10.5357 12.5714 10.3571 13.3036 10.2857 14.3036C10.2857 14.4464 10.3571 14.5179 10.5 14.5179H12.5893C12.7679 14.5179 12.8571 14.4464 12.8571 14.3036C12.8571 13.9107 12.8929 13.5714 12.9643 13.2857C13.0714 12.9643 13.2857 12.6607 13.6071 12.375L14.3571 11.8929C15.0357 11.3929 15.4821 10.9821 15.6964 10.6607Z"
						fill="#1C2133"
					/>
				</svg>
			</button>
</slot>

{#if isOpen}
	<div class="modal">
		<div class="backdrop" on:click={close}></div>
		<div class="modal-content" use:clickOutside on:click_outside={handleClickOutside}>
			<button class="close" on:click={close}>
				<svg width="40" height="40" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path d="M75.756 33.593L66.404 24.245L49.999 40.649L33.593 24.245L24.242 33.593L40.648 49.998L24.242 66.404L33.593 75.755L49.999 59.35L66.404 75.755L75.756 66.404L59.35 49.998L75.756 33.593ZM49.999 100C22.384 100 0 77.613 0 49.998C0 22.387 22.384 0 49.999 0C77.614 0 99.997 22.387 99.997 49.998C99.997 77.613 77.614 100 49.999 100Z" fill="#1C2133"/>
					</svg>					
			</button>
			<h1>OrangeBurrito's D&D Character Viewer</h1>
			<p>this website displays your D&D character sheets from <a href="https://www.aidedd.org/dnd-builder/index.php?l=1" target="_blank">Aidded's Character Builder</a>
				as HTML.
			</p>

			<h2>How do I use it?</h2>

			<p>Create your character with the <a href="https://www.aidedd.org/dnd-builder/index.php?l=1" target="_blank">Aidded's Character Builder</a>, and when you're finished, select the "Generate Character Sheet
				as BBCode format.
			</p>
			<p>Copy the text in the pop-up and paste it into the editor on the left.</p>
			<p>Now you can easily edit it!</p>

			<h2>Site Stats</h2>
			<p><strong>Author</strong> <a href="https://github.com/orangeBurrito" target="_blank">OrangeBurrito</a></p>

			<h3>Dev Dependencies</h3>
			<ul>
				<li><a href="https://github.com/sveltejs/svelte" target="blank">svelte</a></li>
				<li><a href="https://github.com/markedjs/marked" target="blank">marked</a></li>
				<li><a href="https://www.npmjs.com/package/js-bbcode-parser" target="blank">js-bbcode-parser</a></li>
			</ul>

			<br>

			<h2>Upcoming Features (maybe)</h2>
			<ul>
				<li>Synchronized Scrolling</li>
				<li>Save D&D Character Sheets</li>
			</ul>
		</div>
	</div>
{/if}

<svelte:window on:keydown={handleKeyDown}/>

<style>
	.modal-btn {
		padding: 0 1rem;
		cursor: pointer;
		border: none;
		background: none;
	}
	
	
	.modal-btn svg {
		transition: 0.1s ease-out;
		border-radius: 50px;
	}

	.modal-btn svg:hover {
		background: var(--white);
	}

	.modal {
		color: var(--black);
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  .backdrop {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(28, 33, 51, 0.6);
  }
	
	.modal-content {
		z-index: 10;
		width: 60%;
		padding: 1.5rem;
		background: var(--white);
		border-radius: 15px;
		position: relative;
	}

	.close {
		position: absolute;
		right: 0;
		border: none;
		background: none;
		cursor: pointer;
		margin-right: 1rem;
	}

	.close:hover {
		background: #b04a3b;
		border-radius: 100px;
	}
	
	h1 {
		margin-bottom: 0.5rem;
	}
</style>

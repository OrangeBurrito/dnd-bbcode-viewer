<script>
	import Router, {location} from 'svelte-spa-router'

	import Home from './pages/Home.svelte'
	import Form from './pages/Form.svelte'

</script>

<svelte:head>
	<title>D&D Viewer</title>
</svelte:head>

<!-- <nav>
	<a href="">Home</a>
	<a href="/#/form">Form</a>
</nav> -->

<Router routes={{
	'/': Home,
	'/form': Form
}} />
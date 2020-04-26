<script>
	import Nav from '../components/Nav.svelte';

	export let segment;
</script>

<style lang="scss" global>
	@import "./style/global.scss";

	main {
		padding: $space--large;
	}
</style>


<Nav {segment}/>

<main>
	<slot></slot>
</main>
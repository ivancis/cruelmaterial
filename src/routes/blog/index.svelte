<script
context="module">
	export function preload({ params, query }) {
		return this.fetch(`blog.json`).then(r => r.json()).then(posts => {
			return { posts };
		});
	}
</script>

<script>
	export let posts;
</script>

<style lang="scss">
	@import "./style/_config.scss";
	ul {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		max-width: 80vh;
		grid-gap: $space;
		margin: 0;
		padding: 0;
	}

	li {
		@include ratio(1,1);
		background: $_n100;
		border-radius: $space--x-small;
	}

	a {
		display: grid;
		place-content: flex-end;
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		text-decoration: none;
		padding: $space--large;
	}

	label {
		color: $light;
	}
</style>

<svelte:head>
	<title>Blog</title>
</svelte:head>

<ul>
	{#each posts as post}
		<li>
			<a
				rel='prefetch'
				href='blog/{post.slug}'
			>
				<label>
					{post.title}
				</label>
			</a>
		</li>
	{/each}
</ul>

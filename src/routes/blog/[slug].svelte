<script context="module">
	export async function preload({ params, query }) {
		// the `slug` parameter is available because
		// this file is called [slug].svelte
		const res = await this.fetch(`blog/${params.slug}.json`);
		const data = await res.json();

		if (res.status === 200) {
			return { post: data };
		} else {
			this.error(res.status, data.message);
		}
	}
</script>

<script>
	export let post;
</script>

<style lang="scss">
	@import "./style/_config.scss";
	.post {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: $space--x-large;
		align-items: flex-start;
		max-width: $content-size-medium;
	}

	.gallery {
		@include ratio(1,1);
		background: $_n100;
		border-radius: $space--x-small;
	}
	.content {
		display: grid;
		grid-gap: $space;
	}

	.markdown :global(h2) {
		font-size: 1.4em;
		font-weight: 500;
	}

	.markdown :global(pre) {
		background-color: #f9f9f9;
		box-shadow: inset 1px 1px 5px rgba(0,0,0,0.05);
		padding: 0.5em;
		border-radius: 2px;
		overflow-x: auto;
	}

	.markdown :global(pre) :global(code) {
		background-color: transparent;
		padding: 0;
	}

	.markdown :global(ul) {
		line-height: 1.5;
	}

	.markdown :global(li) {
		margin: 0 0 0.5em 0;
	}

	.markdown :global(p) {
		color: red;
	}
</style>

<svelte:head>
	<title>{post.title}</title>
</svelte:head>

<div class="post">
	<div class='gallery'>
	</div>
	<div class='content'>
		<h1>{post.title}</h1>
		<div class='markdown'>
			{@html post.html}
		</div>
		<div class="action">
			hello action
		</div>
	</div>
</div>

<script>
	import { scale } from 'svelte/transition';
	export let id;
	export let name;
	$: url = "https://ndmcweb.github.io?t="+id;

	let copied = false;

	function copy_to_clipboard() {
		navigator.clipboard.writeText(url);
		copied = true;

		setTimeout(()=>{
			copied = false;
		},2500)
	}
</script>

<style>
	.copy-toast {
		position: sticky;
		top: 0;
		left: 0;
		right: 0;
	}
</style>

<tr>
	<td class="is-size-4-mobile">{id}</td>
	<td class="is-size-3-mobile has-text-centered">{name}</td>
	<td class="has-text-centered-mobile">
		{url}
	</td>
	<td class="has-text-centered-desktop">
		<button class="button" on:click={copy_to_clipboard}>
			{#if copied}
				<span class="has-text-link" transition:scale="{{delay: 0, duration: 300}}">Copied</span>
			{:else}
			<span class="icon is-small">
				<figure class="image">
					<img src="/res/copy.png">
				</figure>
			</span>
			{/if}
		</button>
	</td>
</tr>
<script>
	import Navbar from "./Navbar.svelte"
	import TrackerTable from "./TrackerTable.svelte"
	import TrackerMaker from "./TrackerMaker.svelte"
	import CreateButton from "./CreateButton.svelte"
	import RefreshButton from "./RefreshButton.svelte"
	let name = 'world';
	let ui = {
		show_tracker_maker: false,
		show_tracker_table: true
	};
	
	let trackers = [
		["xxxx", "check your"],
		["xxxx", "network connection"],
	];
	let base_url = "https://ndmcweb.pythonanywhere.com";

</script>

<Navbar bind:ui/>

<section class="section pb-0">
<div class="container is-flex">
	<div class="columns ml-auto">
		<div class="column py-3">
			<CreateButton bind:ui/>
		</div>
		<div class="column py-3">
			<RefreshButton bind:ui bind:trackers bind:base_url/>
		</div>
	</div>
</div>
</section>

{#if ui.show_tracker_maker}
	<TrackerMaker bind:ui bind:trackers bind:base_url/>
{/if}

{#if ui.show_tracker_table}
	<TrackerTable bind:trackers bind:base_url/>
{/if}

<section class="section">
	<div class="container has-text-centered has-text-grey is-size-7">
		contributors: cluser404 & ninadgns
	</div>
</section>
<script>
	import { scale } from 'svelte/transition';
	import Tracker from "./Tracker.svelte";
	export let base_url;

	export let trackers;
	console.log("populating table");

	async function fetch_trackers() {
		const response = await fetch(base_url+"/trackers");
		const data = await response.json();
		trackers = data;
		return data;
	}

	fetch_trackers().then(()=>{
		console.log("updated tracker table")
	});
</script>


<section class="section" transition:scale="{{delay: 0, duration: 300}}">
<div class="container has-shadow">
	<div class="b-table">
		<div class="table-wrapper has-mobile-cards">
			<table class="table is-fullwidth is-striped is-hoverable is-fullwidth">
			<thead>
				<tr>
					<th>Tracker</th>
					<th class="has-text-centered">Forwarder</th>
					<th class="has-text-centered-mobile">Link</th>
					<th class="has-text-centered-desktop">Copy Tracker Link</th>
				</tr>
			</thead>
			<tbody>
				{#each trackers as tracker}
					<Tracker id={tracker[0]} name={tracker[1]}/>
				{/each}
			</tbody>
			</table>
		</div>
	</div>
</div>
</section>
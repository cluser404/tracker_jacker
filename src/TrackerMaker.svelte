<script>
	import { scale } from 'svelte/transition';
	export let ui;
	export let trackers;
	export let base_url;

	let error = false;
	let tracker_id = "";
	let data = {forwarder: ""};

	async function fetch_trackers() {
		const response = await fetch(base_url+"/trackers");
		const data = await response.json();
		return data;
	}

	async function post_tracker() {
		const response = await fetch(base_url+"/tracker/"+tracker_id, 
	  	{
	  		method: 'post',	
			headers: {
		    	'Accept': 'application/json, text/plain, */*',
		    	'Content-Type': 'application/json'
		  	},
		  	body: JSON.stringify(data)
		})
	  const res = await response.json();
	  console.log(res);
	  return res;
	}

	function save() {
		if(!Number(tracker_id)) {
			error=true;
		} else {
			post_tracker().then((data)=>{
				if(data.status == "done commiting data to database") {
					fetch_trackers().then((data)=>{
						trackers = data;
					})
					discard();
				} else {
					error = true;
				}
			});
		}
	}

	function discard() {
		ui.show_tracker_maker = false;
	}
</script>

<section class="section" transition:scale="{{delay: 0, duration: 300}}">
	<div class="container">
		<div class="card">
			<div class="card-content">
				<h2 class="is-size-5 has-text-weight-bold mb-0">Tracker Maker</h2>
				<h3 class="is-size-6 has-text-weight-bold has-text-grey mb-5 mt-0">Create a tracker jacker</h3>

				<div class="mb-1">
					<label class="has-text-weight-medium mb-2">Unique Tracker Id</label>
					{#if error}
					<span class="tag is-danger is-light ml-2">must be a unique number</span>
					{/if}
				</div>
				<input bind:value={tracker_id} class="input mb-5" type="text" placeholder="anything unique like - 7345 or 2344">
				
				<div class="mb-1">
					<label class="has-text-weight-medium mb-2">Name of Tracker Forwarder</label>
				</div>
				<input bind:value={data.forwarder} class="input mb-5" type="text" placeholder="Awesome Preacher">
			</div>
			<footer class="card-footer">
				<button on:click={save} class="card-footer-item button has-text-weight-medium">Save</button>
				<button
					class="card-footer-item button has-text-weight-medium"
					on:click={discard}>
					Discard
				</button>
			</footer>
		</div>
	</div>
</section>
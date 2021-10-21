<script>
	export let ui;
</script>

<button 
  class="button is-small is-link has-text-weight-bold is-fullwidth"
  on:click={()=>{ui.show_tracker_maker = !ui.show_tracker_maker}}>
  CREATE NEW TRACKER
</button>
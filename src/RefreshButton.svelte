<script>
  export let ui;
  export let trackers;
  export let base_url;

  async function fetch_trackers() {
    const response = await fetch(base_url+"/trackers");
    const data = await response.json();
    trackers = data;
    return data;
  }

  function refresh_table() {
    fetch_trackers().then(()=>{
      console.log("done refreshing table")
    });
  }
</script>

<button 
  class="button is-small has-text-weight-bold is-fullwidth"
  on:click={refresh_table}>
  REFRESH TRACKER DATA
</button>
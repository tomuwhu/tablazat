<script>
  import { onMount } from "svelte";
  let data = []
  const apikey = 'ngPn3mJPG4y7T1HGBUMzhsSYQRRdwmaRzpaJap06'
  onMount(async () => {
    data = await fetch(`https://api.nasa.gov/neo/rest/v1/feed?start_date=2024-10-24&end_date=2024-10-25&api_key=${apikey}`)
    data = (await data.json()).near_earth_objects['2024-10-24']
    console.log(data)
  })
</script>

<main>
  <table>
    {#each data as item}
      <tr>
        <td>{item.name}</td>
      </tr>
    {/each}
  </table>
</main>

<style>
 
</style>

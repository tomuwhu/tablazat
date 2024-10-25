<script>
  import { onMount } from "svelte";
    import { get } from "svelte/store";
  let data = []
  let datum = '2024-10-24'
  const apikey = 'ngPn3mJPG4y7T1HGBUMzhsSYQRRdwmaRzpaJap06'
  const getData =async() => {
    data = await fetch(`https://api.nasa.gov/neo/rest/v1/feed?start_date=${datum}&end_date=${datum}&api_key=${apikey}`)
    data = (await data.json()).near_earth_objects[datum]
    console.log(data)
  }
  onMount(() => {
    getData()
  })
</script>

<main>
  <input type="date" bind:value={datum} 
    min="2015-01-01" max="2024-10-24"
    on:change={() => getData()}/>
  {#if data.length > 0}
  <table>
    {#each data as item}
      <tr>
        <td>{item.name}</td>
        <td>{item.estimated_diameter.kilometers.estimated_diameter_min}</td>
        <td>{item.estimated_diameter.kilometers.estimated_diameter_max}</td>
      </tr>
    {/each}
  </table>
  {/if}
</main>

<style>
 table {
   border-collapse: collapse;
 }
 td {
   border: 1px solid black;
   padding: 5px;
   text-align: left;
 }
</style>

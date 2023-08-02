<script>
  import { onMount } from "svelte";

  let data = null;

  const fetchData = async () => {
    try {
      const response = await fetch("https://dog.ceo/api/breeds/image/random");
      if (!response.ok) {
        throw new Error("Network response was not ok");
      }
      data = await response.json();
      console.log(data);
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  };

  onMount(() => {
    fetchData(); // Fetch data when the component is mounted initially
  });
</script>

<main>
  <h1>Sjå på denne, då!</h1>

  {#if data}
    <button on:click={fetchData}>Ny hund!</button>
    <br />
    <img src={data.message} alt="A dog" class="max-image-size" />
  {:else}
    <p>Loading...</p>
  {/if}
</main>

<style>
  .max-image-size {
    margin: 40px;
    max-width: 500px;
    max-height: 400px;
    height: auto; /* Ensures the aspect ratio is maintained */
  }
</style>

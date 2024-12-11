<script>
  let latitude = 0;
  let longitude = 0;
  let roofPrice = 750; // per square price of roof in usd

  const calculateRoofPrice = () => {
    // Simplified calculation, replace with your logic
    roofPrice = parseFloat(latitude) + parseFloat(longitude);
  };

  const handleSubmit = (event) => {
    event.preventDefault(); // Prevents the default form submission and page reload
    calculateRoofPrice();
  };
</script>

<main>
  <h1>Roofing Calculator</h1>

  <form on:submit={handleSubmit}>
    <!-- <label for="latitude">Latitude:</label>
    <input type="number" bind:value={latitude} />

    <label for="longitude">Longitude:</label>
    <input type="number" bind:value={longitude} /> -->

    <label for="sqrft">sqrft:</label>
    <input type="number" bind:value={longitude} />

    <button type="submit">Calculate</button>
  </form>

     <div>
      <h2>Estimated Roof Price:</h2>
      <p>${roofPrice}</p>
    </div>
 </main>

<style>
  /* Use Tailwind CSS classes for styling */
</style>

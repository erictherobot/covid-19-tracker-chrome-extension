<script>
  const fetchData = (async () => {
    const response = await fetch(
      'https://covid-193.p.rapidapi.com/statistics',
      {
        method: 'GET',
        headers: {
          'x-rapidapi-host': 'covid-193.p.rapidapi.com',
          'x-rapidapi-key':
            'W1IchbXbLHmshIRtLntY6jRvsY8Lp12EOmXjsnoVnOaRIjxNiq',
        },
      }
    )
    return await response.json()
  })()
</script>

<style>
  * {
    font-size: 1.125rem;
    line-height: 1.5;
  }
  .list {
    padding: 10px;
    background-color: rgb(248, 219, 239);
    margin: 0 auto 20px auto;
    min-width: 400px;
    border-radius: 4px;
  }
  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  h3 {
    margin: 0px auto 5px;
    padding: 0;
  }
  p {
    padding: 10px;
    margin: 0 auto 20px auto;
    min-width: 400px;
  }
  .spinner:before {
    content: '';
    box-sizing: border-box;
    position: absolute;
    top: 50%;
    left: 50%;
    width: 25px;
    height: 25px;
    margin-top: -10px;
    margin-left: -10px;
    border-radius: 50%;
    border: 4px solid #f6f;
    border-top-color: #0e0;
    border-right-color: #0dd;
    border-bottom-color: #f90;
    animation: spinner 0.6s linear infinite;
  }
  .spinner {
    position: relative;
    min-height: 36px;
    background: #fff;
    margin: 10px 20px 0 0;
  }
  img {
    width: 25px;
    vertical-align: middle;
  }
  a {
    color: #333;
    text-decoration: underline;
  }
  @keyframes spinner {
    to {
      transform: rotate(360deg);
    }
  }
</style>

<h3>COVID-19 Updates</h3>

{#await fetchData}
  <p>
    <span class="spinner" />
    ...fetching COVID-19 updates
  </p>
{:then data}
  {#each data.response as { country, cases, deaths }, i}
    <div class="list">
      <h3>{country}</h3>
      <ul>
        <li>New: {cases.new}</li>
        <li>Active: {cases.active}</li>
        <li>Critical: {cases.critical}</li>
        <li>Recovered: {cases.recovered}</li>
        <li>Recent Deaths: {deaths.new}</li>
        <li>Total Deaths: {deaths.total}</li>
      </ul>
    </div>
  {/each}
{:catch error}
  <p>An error occurred!</p>
{/await}
<footer>
  <p>
    Made by
    <a href="https://colorfuldots.com" target="_blank">
      <img
        src="https://svelte-firestore-todos.erictherobot.now.sh/colorful-dots-llc.png"
        alt="Colorful Dots, LLC" />
    </a>
    using
    <a href="https://svelte.dev" target="_blank">Svelte</a>
  </p>
</footer>

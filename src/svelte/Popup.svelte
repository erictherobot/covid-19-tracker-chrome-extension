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
    background-color: #fff1fb;
    border: 1px dotted #f6f;
    margin: 10px auto 10px auto;
    min-width: 300px;
    border-radius: 4px;
  }
  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  h1 {
    margin: 0 auto 0;
    padding: 0;
    font-size: 1.2rem;
  }
  h3 {
    margin: 0 auto 5px;
    padding: 0;
  }
  .spinner-wrapper {
    padding: 10px;
    margin: 0 auto 20px auto;
    min-width: 300px;
    text-align: center;
  }
  .spinner:before {
    content: '';
    box-sizing: border-box;
    position: absolute;
    top: 50%;
    left: 50%;
    width: 30px;
    height: 30px;
    margin-top: -5px;
    margin-left: -15px;
    margin-bottom: 10px;
    border-radius: 50%;
    border: 4px solid #f6f;
    border-top-color: #0e0;
    border-right-color: #0dd;
    border-bottom-color: #f90;
    animation: spinner 0.5s linear infinite;
  }
  .spinner {
    position: relative;
    min-height: 36px;
    background: #fff;
    margin: 10px 0 0 0;
  }
  img {
    width: 45px;
    vertical-align: middle;
  }
  a {
    color: #f6f;
    text-decoration: underline;
    font-size: 15px;
  }
  hr {
    background: linear-gradient(to right, #f6f, #0dd);
    height: 4px;
    border: 0;
  }
  footer {
    text-align: center;
  }
  footer p {
    font-size: 14px;
    color: #656565;
  }
  @keyframes spinner {
    to {
      transform: rotate(360deg);
    }
  }
</style>

<h1>Global COVID-19 Updates</h1>
<hr />

{#await fetchData}
  <div class="spinner-wrapper">
    <span class="spinner" />
  </div>
{:then data}
  {#each data.response as { country, cases, deaths }, i}
    <div class="list">
      <h3>{country}</h3>
      <ul>
        <li>
          <strong>New:</strong>
          {cases.new}
        </li>
        <li>
          <strong>Active:</strong>
          {cases.active}
        </li>
        <li>
          <strong>Critical:</strong>
          {cases.critical}
        </li>
        <li>
          <strong>Recovered:</strong>
          {cases.recovered}
        </li>
        <li>
          <strong>Recent Deaths:</strong>
          {deaths.new}
        </li>
        <li>
          <strong>Total Deaths:</strong>
          {deaths.total}
        </li>
      </ul>
    </div>
    <hr />
  {/each}
{:catch error}
  <p>An error occurred!</p>
{/await}
<footer>
  <p>
    <a href="https://colorfuldots.com" target="_blank">
      <img
        src="https://svelte-firestore-todos.erictherobot.now.sh/colorful-dots-llc.png"
        alt="Colorful Dots, LLC" />
    </a>
    <br />
    <br />
    &copy;2020 Colorful Dots, LLC
  </p>
</footer>

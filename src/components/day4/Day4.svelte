<script>
  import Waffle from "./Waffle.svelte";
  import data from "./data.json";
  import logo from "./logo.svg";
  import { scaleOrdinal } from "d3";
  import sudesteMap from "./sudeste.png";
  import nordesteMap from "./nordeste.png";
  import sulMap from "./sul.png";
  import norteMap from "./norte.png";
  import centrooesteMap from "./centrooeste.png";

  export let width;
  export let height;

  const colorRange = ["#F895CC", "#DC120E", "#F99506", "#703EA0", "#209168"];

  const colorScale = scaleOrdinal()
    .domain([data.map((e) => e.region)])
    .range(colorRange);

  const mapRange = [sudesteMap, nordesteMap, sulMap, norteMap, centrooesteMap];
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>The great disparities of population between the regions of Brazil</h2>
    <p>
      More than 200 millions of people live in Brazil. The most populated region
      is the Sudeste, which includes the cities of Rio de Janeiro and São Paulo.
    </p>
  </div>

  <div class="chart">
    {#each data as region, i}<Waffle
        data={region}
        {colorScale}
        map={mapRange[i]}
      />
    {/each}
  </div>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Instituto Brasileiro de Geografia e Estatística</p>
      </div>
      <p class="challenge">#30DayChartChallenge 2024</p>
    </div>
    <img src={logo} alt="wild variables logo" class="logo" />
  </div>
</div>

<style>
  .chart-container {
    background-color: #fffaf3;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  .intro {
    padding: 3vh;
  }

  .intro p {
    margin-bottom: 0px;
  }

  h2 {
    font-family: "Londrina Solid", sans-serif;
    font-weight: 400;
    font-size: 2rem;
    margin: 0px 0px;
  }

  p {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
  }

  .chart {
    display: flex;
    gap: 15px;
    justify-content: center;
  }

  .footer {
    display: flex;
    justify-content: space-between;
    align-items: end;
    padding: 3vh;
    padding-top: 6px;
    gap: 70px;
  }

  .footer-infos {
    display: flex;
    flex-direction: column;
    justify-content: end;
    align-items: flex-start;
    gap: 4px;
  }

  .footer-infos p {
    margin: 0;
  }

  .comment p {
    font-size: 12px;
    margin: 0;
  }

  .challenge {
    background-color: #172529;
    color: #fffaf3;
    padding: 2px 6px;
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
  }

  .logo {
    width: 130px;
  }
</style>

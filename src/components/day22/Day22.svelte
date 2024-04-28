<script>
  import logo from "./logo.svg";
  import { scaleLinear, interpolatePlasma } from "d3";
  import data from "./data.json";

  export let width;
  export let height;
  $: chartHeight = height / 1.6;
  $: chartWidth = width - 50;

  // Scales
  $: xScale = scaleLinear()
    .domain([0, 14000000])
    .range([40, chartWidth - 15]);
  $: yScale = scaleLinear()
    .domain([0, 800])
    .range([chartHeight - 55, 35]);
  const colorScale = scaleLinear().domain([0, 22]).range([1, 0]);

  const yTicks = [800, 700, 600, 500, 400, 300, 200, 100, 0];
  const xTicks = [
    0, 2000000, 4000000, 6000000, 8000000, 10000000, 12000000, 14000000,
  ];
  const legend = Array.from({ length: 150 });
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>Brasília stands out in cycling infrastructures</h2>
    <div class="text-intro">
      <p>
        Among the ten most populated cities in Brazil, Brasília has implemented
        the most cycle paths and lanes relative to its population.
      </p>
      <div class="annotations">
        <div style="line-height: 110%;">
          Km of cycle paths and lanes for 100k inhabitants
        </div>

        <div class="legend">
          {#each legend as _, i}
            <div
              class="tone"
              style="height: 8px; width: 1px; background-color: {interpolatePlasma(
                i / legend.length
              )}"
            ></div>
          {/each}
        </div>
        <div class="text-annotations">
          <div>22km</div>
          <div>11km</div>
          <div>0km</div>
        </div>
      </div>
    </div>
  </div>

  <svg width={chartWidth} height={chartHeight}>
    <!-- Axis -->
    <g class="axis-x">
      {#each xTicks as tick}
        <text x={xScale(tick)} y={chartHeight - 35} text-anchor="middle"
          >{Math.round(tick / 1000000) + "M"}</text
        >
        <line
          x1={xScale(tick)}
          x2={xScale(tick)}
          y1={chartHeight - 55}
          y2={35}
          stroke="#b9b9b9"
          stroke-width={tick === 0 ? "2" : "0.5"}
          stroke-opacity={tick === 0 ? "1" : "0.8"}
        />
      {/each}
      <text
        class="axis-title"
        x={xScale(14300000)}
        y={chartHeight - 25}
        text-anchor="end"
        dominant-baseline="hanging">City population →</text
      >
    </g>
    <g class="axis-y">
      {#each yTicks as tick}
        <g class="tick">
          {#if tick % 200 === 0}
            <text
              x="15"
              y={yScale(tick)}
              text-anchor="middle"
              dominant-baseline="middle">{tick}</text
            >
          {/if}
          <line
            x1="40"
            x2={chartWidth - 15}
            y1={yScale(tick)}
            y2={yScale(tick)}
            stroke="#b9b9b9"
            stroke-width={tick === 0 ? "2" : "0.5"}
            stroke-opacity={tick === 0 ? "1" : "0.8"}
          />
        </g>
      {/each}
      <text class="axis-title" x="0" y="10" dominant-baseline="middle"
        >↑ Km of cycle paths and cycle lanes</text
      >
    </g>
    <!-- Graph -->
    {#each data as city}
      <circle
        class={city.city}
        cx={xScale(city.pop)}
        cy={yScale(city.ciclovias)}
        r="8"
        fill={interpolatePlasma(colorScale(city.for_100mil))}
        opacity="0.8"
      />
      <text
        x={city.city === "São Paulo (SP)"
          ? xScale(city.pop) - 12
          : xScale(city.pop) + 12}
        y={yScale(city.ciclovias)}
        dominant-baseline="middle"
        text-anchor={city.city === "São Paulo (SP)" ? "end" : "start"}
        style="font-size : {11 + city.for_100mil / 5}px">{city.city}</text
      >
    {/each}</svg
  >

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Alianca Bike, 2023</p>
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
    color: #172529;
  }

  .intro {
    padding: 3vh;
  }

  h2 {
    font-family: "Londrina Solid", sans-serif;
    font-weight: 400;
    font-size: 2rem;
    margin: 0px 0px;
  }

  p,
  text {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
  }

  .intro p {
    margin-bottom: 0px;
    margin-top: 0px;
  }

  .text-intro {
    display: flex;
    align-items: center;
    margin-top: 6px;
  }

  .text-intro > p {
    padding-right: 30px;
  }

  .annotations {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 300px;
    gap: 5px;
    font-family: "Poppins", sans-serif;
    font-size: 12px;
  }

  .legend {
    display: flex;
    padding-left: 10px;
    padding-right: 10px;
  }

  .text-annotations {
    display: flex;
    justify-content: space-between;
    width: 170px;
  }

  svg {
    padding: 0 3vh;
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

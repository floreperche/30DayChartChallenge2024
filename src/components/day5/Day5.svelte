<script>
  import logo from "./logo.svg";
  import { scaleLinear, line, curveBumpX } from "d3";
  import data from "./data.json";
  import AxisX from "./AxisX.svelte";
  import AxisY from "./AxisY.svelte";

  export let width;
  export let height;
  $: chartHeight = height / 1.6;
  $: chartWidth = width - 50;

  // Scales
  const xScale = scaleLinear()
    .domain([2014, 2023])
    .range([40, width - 135]);
  $: yScale = scaleLinear()
    .domain([1, 23])
    .range([30, chartHeight - 35]);

  // Line generations
  const lineGremioGenerator = line()
    .x((d) => xScale(d.year))
    .y((d) => yScale(d.gremio))
    .curve(curveBumpX);
  const lineInterGenerator = line()
    .x((d) => xScale(d.year))
    .y((d) => yScale(d.inter))
    .curve(curveBumpX);
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>
      The <span style="color : #0884BD">Gremio</span> vs.
      <span style="color : #E4050F">Inter</span> rivality
    </h2>
    <div class="description">
      <p>
        Gremio and Inter are the two famous, historic and rival brazilian
        football clubs of the city of Porto Alegre. Surprisingly, their average
        rankings in the Brasileirão Série A Championship over the last decade
        are nearly identical.
      </p>
      <div class="legend">
        <p>Average ranking</p>
        <p>
          <svg width="30" height="10" style=" padding:0px"
            ><line
              x1="0"
              x2="25"
              y1="5"
              y2="5"
              stroke="#0884BD"
              stroke-width="2"
              stroke-dasharray="8"
            /></svg
          ><span style="color : #0884BD">Gremio: 6.22</span>
        </p>
        <p>
          <svg width="30" height="10" style=" padding:0px"
            ><line
              x1="0"
              x2="25"
              y1="5"
              y2="5"
              stroke="#E4050F"
              stroke-width="2"
              stroke-dasharray="8"
            /></svg
          ><span style="color : #E4050F">Inter: 6.66</span>
        </p>
      </div>
    </div>
  </div>

  <svg width={chartWidth} height={chartHeight}>
    <AxisY {yScale} {xScale} />
    <!-- Lines -->
    <!-- Gremio -->
    <path
      fill="none"
      stroke="#0884BD"
      stroke-width="4"
      d={lineGremioGenerator(data)}
    />
    <!-- Inter -->
    <path
      fill="none"
      stroke="#E4050F"
      stroke-width="4"
      d={lineInterGenerator(data)}
    />
    <!-- Circles -->
    <g>
      {#each data as year}
        <g>
          <!-- Gremio -->
          <circle
            cx={xScale(year.year)}
            cy={yScale(year.gremio)}
            r={8 / year.gremio + 9}
            fill="white"
            stroke="black"
            stroke-width="2"
          />
          <circle
            cx={xScale(year.year)}
            cy={yScale(year.gremio)}
            r={8 / year.gremio + 6}
            fill="#0884BD"
          />

          <!-- Inter -->
          <circle
            cx={xScale(year.year)}
            cy={yScale(year.inter)}
            r={8 / year.inter + 9}
            fill="white"
            stroke="#E4050F"
            stroke-width="2"
          />
          <circle
            cx={xScale(year.year)}
            cy={yScale(year.inter)}
            r={8 / year.inter + 6}
            fill="#E4050F"
          />
        </g>
      {/each}
    </g>
    <AxisX width={chartWidth} {data} {xScale} {yScale} />
    <!-- Annotations -->
    <g>
      <text
        x={xScale(2023.5)}
        y={yScale(2)}
        text-anchor="start"
        dominant-baseline="middle"
        fill="#0884BD"
        class="name">Gremio</text
      >
      <text
        x={xScale(2023.5)}
        y={yScale(9)}
        text-anchor="start"
        dominant-baseline="middle"
        fill="#E4050F"
        class="name">Inter</text
      >
      <g>
        <text
          x={xScale(2024.1)}
          y={yScale(19)}
          text-anchor="middle"
          dominant-baseline="middle"
          class="annotation"
          fill="#b9b9b9">Relegation</text
        >
        <text
          x={xScale(2024.1)}
          y={yScale(20)}
          text-anchor="middle"
          dominant-baseline="middle"
          class="annotation"
          fill="#b9b9b9">to Série B</text
        ><text
          x={xScale(2024.1)}
          y={yScale(21)}
          text-anchor="middle"
          dominant-baseline="middle"
          class="annotation"
          fill="#b9b9b9">▼</text
        ></g
      >
    </g>
  </svg>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Confederação Brasileira de Futebol</p>
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
    margin-bottom: 0px;
  }

  .description {
    display: flex;
    justify-content: space-between;
    gap: 30px;
  }

  .legend {
    display: flex;
    flex-direction: column;
    padding-top: 14px;
    padding-right: 4px;
    width: 390px;
    gap: 10px;
  }

  .legend p {
    margin: 0;
    font-size: 12px;
  }
  .legend span {
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
  }

  svg {
    /* background-color: aquamarine; */
    padding: 0px 25px;
  }

  .name {
    font-family: "Londrina Solid", sans-serif;
    font-size: 20px;
  }

  .annotation {
    font-family: "Poppins", sans-serif;

    font-size: 12px;
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

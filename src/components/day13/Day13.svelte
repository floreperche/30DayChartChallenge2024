<script>
  import logo from "./logo.svg";
  import data from "./data.json";
  import { scaleLinear, line, curveCardinal } from "d3";

  export let width;
  export let height;
  $: chartHeight = height / 1.8;
  $: chartWidth = width - 50;

  // Scales
  $: xScale = scaleLinear()
    .domain([1950, 2021])
    .range([50, chartWidth - 10]);
  $: yScale = scaleLinear()
    .domain([0, 25])
    .range([chartHeight - 50, 40]);

  // Line generations
  const lineBrazilGenerator = line()
    .x((d) => xScale(d.year))
    .y((d) => yScale(d.brazil))
    .curve(curveCardinal.tension(0.4));
  const lineWorldGenerator = line()
    .x((d) => xScale(d.year))
    .y((d) => yScale(d.world))
    .curve(curveCardinal.tension(0.4));

  const yTicks = [25, 20, 15, 10, 5, 0];
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>Saving lives, through Child mortality rate plunge</h2>
    <p>
      In seventy years, Child mortality rate* dropped down in Brazil - from <span
        >21%</span
      >
      in 1950 to <span>1.4%</span> in 2021 - slightly faster than the World pace
      (<span class="world">3.7%</span>
      in 2021).
    </p>
  </div>

  <svg width={chartWidth} height={chartHeight}>
    <!-- Axes -->
    <g class="axis-x">
      {#each data as tick}
        {#if tick.year % 10 === 0}
          <g
            class="tick"
            transform="translate({xScale(tick.year)} {chartHeight})"
          >
            <text x="0" y="-25" text-anchor="middle">{tick.year}</text>
          </g>
        {/if}
      {/each}
      <text
        class="axis-title"
        x={xScale(2022.5)}
        y={chartHeight - 15}
        text-anchor="end"
        dominant-baseline="hanging">Year →</text
      >
    </g>
    <g class="axis-y">
      {#each yTicks as tick}
        <g class="tick">
          <text
            x="15"
            y={yScale(tick)}
            text-anchor="middle"
            dominant-baseline="middle">{tick}%</text
          >
          <line
            x1="45"
            x2={chartWidth}
            y1={yScale(tick)}
            y2={yScale(tick)}
            stroke="#b9b9b9"
            stroke-width="0.4"
          />
        </g>
      {/each}
      <text class="axis-title" x="0" y="10" dominant-baseline="middle"
        >↓ Child mortality rate*</text
      >
    </g>
    <!-- Annotations -->
    <text
      x={xScale(1977)}
      y={yScale(7)}
      text-anchor="middle"
      dominant-baseline="middle"
      class="annotations"
      fill="#209168">Brazil</text
    >
    <text
      x={xScale(1990)}
      y={yScale(12)}
      text-anchor="middle"
      dominant-baseline="middle"
      class="annotations"
      fill="#b8d9c6">World</text
    >
    <!-- Graph -->

    <!-- Worl -->
    <path
      fill="none"
      stroke="#b8d9c6"
      stroke-width="4"
      d={lineWorldGenerator(data)}
      stroke-linecap="round"
    />
    <!-- Brazil -->
    <path
      fill="none"
      stroke="#209168"
      stroke-width="6"
      d={lineBrazilGenerator(data)}
      stroke-linecap="round"
    />
  </svg>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>*Share of children who died before reaching the age of 5</p>
        <p>Source: United Nations via Our World in Data</p>
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

  p,
  text {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
  }

  .intro p {
    margin-bottom: 0px;
  }

  span {
    font-family: "Londrina Solid", sans-serif;
    font-size: 18px;
    background-color: #209168;
    color: #fffaf3;
    padding: 1px 3px;
  }

  .world {
    background-color: #b8d9c6;
    color: #172529;
  }

  svg {
    margin-left: 3vh;
  }

  .annotations {
    font-family: "Londrina Solid", sans-serif;
    font-size: 20px;
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
    background-color: #209168;
    color: #fffaf3;
    padding: 2px 6px;
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
  }

  .logo {
    width: 130px;
  }
</style>

<script>
  import logo from "./logo.svg";
  import data from "./data.json";
  import { scaleBand, scaleLinear, scaleOrdinal } from "d3";

  export let width;
  export let height;
  $: chartHeight = height / 1.7;
  $: chartWidth = width - 50;

  let players = [];
  $: data.map((e) => {
    players.push(e.name);
  });

  // Scales
  $: xScale = scaleBand()
    .domain(players)
    .range([50, chartWidth + 40]);
  $: yGoalScale = scaleLinear()
    .domain([0, 120])
    .range([chartHeight - 130, 35]);
  $: xAverageScale = scaleLinear()
    .domain([0, 1])
    .range([0, xScale.bandwidth() - 48]);
  const colorRange = ["#209168", "#F4DC23"];
  const colorScale = scaleOrdinal().domain(["w", "m"]).range(colorRange);

  $: ticks = yGoalScale.ticks(6);
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>Marta, the top goal scorer of Brazil national football teams</h2>
    <div>
      <div>
        <div style="width: 20px; height:20px; background-color: #209168"></div>
        <p>Member of Brazil women's national football team</p>
      </div>
      <div>
        <div style="width: 20px; height:20px; background-color: #F4DC23"></div>
        <p>Member of Brazil men's national football team</p>
      </div>
    </div>
  </div>

  <svg width={chartWidth} height={chartHeight}>
    <!-- Axis -->
    <g>
      <text x="4" y="10" dominant-baseline="middle"
        >↑ Number of goals scored with Brazil National team</text
      >

      {#each ticks as tick}
        {#if tick % 40 === 0}
          <text
            x="15"
            y={yGoalScale(tick)}
            dominant-baseline="middle"
            text-anchor="middle">{tick}</text
          >
        {:else}
          <line
            x1="12"
            y1={yGoalScale(tick)}
            x2="18"
            y2={yGoalScale(tick)}
            stroke="#172529"
            stroke-width="1"
          />
        {/if}
      {/each}
    </g>
    <g>
      <text
        x={chartWidth / 2}
        y={chartHeight - 15}
        dominant-baseline="middle"
        text-anchor="middle">Average goal scored by match</text
      >
    </g>

    <!-- Chart -->
    {#each data as player}
      <!-- Bar chart -->
      <rect
        x={xScale(player.name)}
        y={yGoalScale(player.goals)}
        width={xScale.bandwidth() - 40}
        height={yGoalScale(0) - yGoalScale(player.goals)}
        fill={colorScale(player.genre)}
      />
      <text
        x={xScale(player.name) + (xScale.bandwidth() - 40) / 2}
        y={yGoalScale(player.goals) + 35}
        text-anchor="middle"
        fill={player.genre === "w" ? "#fffaf3" : "#3d484b"}
        fill-opacity="0.8"
        class="result">{player.goals}</text
      >
      <text
        x={xScale(player.name) + (xScale.bandwidth() - 40) / 2}
        y={chartHeight - 90}
        text-anchor="middle"
        class="names">{player.name}</text
      >
      <!-- Average goal chart -->
      <g>
        <rect
          x={xScale(player.name) + 4}
          y={chartHeight - 60}
          width={xScale.bandwidth() - 48}
          height="10"
          fill="#F2DBB7"
          rx="4"
        />
        <rect
          x={xScale(player.name) + 4}
          y={chartHeight - 60}
          width={xAverageScale(player.average)}
          height="10"
          fill="#0D6CD6"
          rx="4"
        />
        <text
          x={xScale(player.name) + (xScale.bandwidth() - 40) / 2}
          y={chartHeight - 35}
          text-anchor="middle">{player.average}</text
        >
      </g>
    {/each}</svg
  >

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Wikipedia</p>
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
  }

  .intro p {
    margin-bottom: 0px;
    margin-top: 0px;
    font-size: 12px;
  }

  .intro > div {
    display: flex;
    gap: 65px;
    padding-top: 15px;
    justify-content: center;
    padding-left: 30px;
  }

  .intro > div > div {
    display: flex;
    gap: 10px;
    align-items: center;
    width: 50%;
  }

  .intro > div > div p {
    width: 100%;
  }

  svg {
    padding-left: 3vh;
  }

  svg text {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
  }

  .names {
    font-family: "Londrina Solid", sans-serif;
    font-size: 18px;
  }

  .result {
    font-weight: 600;
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

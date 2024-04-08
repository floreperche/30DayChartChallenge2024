<script>
  import logo from "./logo.svg";
  import data from "./data.json";
  import { scaleLinear, scaleOrdinal } from "d3";

  export let width;
  export let height;
  $: chartHeight = height / 1.45;
  $: chartWidth = width - 50;

  // Scales
  $: xScale = scaleLinear().domain([1900, 2000]).range([200, chartWidth]);
  $: yScale = scaleLinear()
    .domain([1, 10])
    .range([20, chartHeight - 90]);
  const styles = ["Choro", "Forró", "Bossa nova", "Samba", "MPB", "Tropicália"];
  const colorRange = [
    "#45D5D1",
    "#F99506",
    "#F895CC",
    "#801FDD",
    "#FC4873",
    "#209168",
  ];
  let colorScale = scaleOrdinal().domain(styles).range(colorRange);

  $: ticks = xScale.ticks(6);
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>
      Top 10 of the best brazilian songs ever <span
        >(according to Rolling Stone)</span
      >
    </h2>
  </div>

  <!-- Legend -->
  <svg {width} height="40">
    {#each styles as style, i}
      <g
        transform="scale(0.65), translate({i * (chartWidth / 3.8)}, 0)"
        class="legend"
      >
        <circle cx="60" cy="18" r="18" fill="url(#gradient1)" />
        <circle cx="60" cy="18" r="18" fill="url(#gradient2)" />
        <circle cx="60" cy="18" r="9" fill={colorScale(style)} />
        <circle cx="60" cy="18" r="2" fill="#fffaf3" />
        <text x="84" y="18" dominant-baseline="middle">{style}</text></g
      >
    {/each}
  </svg>

  <svg {width} height={chartHeight}>
    <radialGradient id="gradient1" cx="50%" cy="50%" r="50%" fx="28%" fy="92%">
      <stop offset="0%" style="stop-color:#869194;" />
      <stop offset="40%" style="stop-color:#172529;" />
    </radialGradient>
    <radialGradient id="gradient2" cx="50%" cy="50%" r="50%" fx="75%" fy="15%">
      <stop offset="0%" style="stop-color:#869194;" />
      <stop offset="40%" style="stop-color:#fffaf300;" />
    </radialGradient>
    <!-- Axis X -->
    <g class="axes">
      {#each ticks as tick}
        <g transform="translate({xScale(tick)}, 0)">
          <text x="0" y={chartHeight - 50} text-anchor="middle">{tick}</text>
          <line x1="0" x2="0" y1="0" y2={chartHeight - 70} stroke="#b9b9b9" />
        </g>
      {/each}
      <text x={chartWidth + 20} y={chartHeight - 30} text-anchor="end"
        >Release date →</text
      >
    </g>
    <!-- AxisY -->

    {#each data as song, i}
      <g class="axes">
        <text
          x="40"
          y={yScale(song.id)}
          dominant-baseline="middle"
          text-anchor="end"
          class="rank">{song.id}</text
        >
        <text x="50" y={yScale(song.id) - 5} dominant-baseline="middle"
          >{song.title}</text
        >
        <text
          x="50"
          y={yScale(song.id) + 10}
          dominant-baseline="middle"
          class="singer"
        >
          {song.singer}</text
        ></g
      >
      <!-- <line
        x1="200"
        x2={xScale(song.year) - 4}
        y1={yScale(song.id)}
        y2={yScale(song.id)}
        stroke="#b9b9b9"
      /> -->
      <!-- Circles -->
      <circle
        cx={xScale(song.year)}
        cy={yScale(song.id)}
        r="18"
        fill="url(#gradient1)"
      />
      <circle
        cx={xScale(song.year)}
        cy={yScale(song.id)}
        r="18"
        fill="url(#gradient2)"
      />
      <circle
        cx={xScale(song.year)}
        cy={yScale(song.id)}
        r="9"
        fill={colorScale(song.style)}
      />
      <circle
        cx={xScale(song.year)}
        cy={yScale(song.id)}
        r="2"
        fill="#fffaf3"
      />
    {/each}
  </svg>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Rolling Stone Brasil, 2009</p>
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
    padding-bottom: 1vh;
  }

  h2 {
    font-family: "Londrina Solid", sans-serif;
    font-weight: 400;
    font-size: 2rem;
    margin: 0px 0px;
  }

  h2 span {
    font-size: 1.6rem;
  }

  p,
  .axes,
  .legend {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
  }

  .singer {
    font-size: 12px;
  }

  .legend {
    font-size: 16px;
  }

  .rank {
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

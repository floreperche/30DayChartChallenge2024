<script>
  import logo from "./logo.svg";
  import round from "./round.png";
  import {
    forceSimulation,
    forceX,
    forceY,
    forceCollide,
    scaleLinear,
    scaleBand,
    scaleOrdinal,
  } from "d3";

  import data from "./data.json";

  export let width;
  export let height;
  $: chartHeight = height / 1.8;
  $: chartWidth = width - 50;

  const radius = 10;

  let simulation = forceSimulation(data);
  let nodes = [];
  simulation.on("tick", () => {
    nodes = simulation.nodes();
  });

  $: {
    simulation
      .force(
        "x",
        forceX()
          .x((d) => xScale(d.size))
          .strength(0.8)
      )
      .force(
        "y",
        forceY()
          .y((d) => yScale(d.food))
          .strength(0.6)
      )
      .force("collide", forceCollide().radius(radius))
      .alpha(0.2)
      .alphaDecay(0.0005)
      .restart();
  }

  $: xScale = scaleLinear().domain([0, 40]).range([150, chartWidth]);

  const food = ["Herbivore", "Omnivore, almost herbivore", "Carnivore"];

  $: yScale = scaleBand().domain(food).range([chartHeight, 50]);

  const colorRange = ["#209168", "#FC4873", "#F99506"];
  let colorScale = scaleOrdinal().domain(food).range(colorRange);

  $: ticks = xScale.ticks(5);
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>What do piranhas eat?</h2>
    <p>
      Contrary to popular belief, piranhas, which are mainly present in South
      America's rivers, consist of a variety of species with diverse diets.
      Attacks on human being are very rare.
    </p>
    <p class="annotation">
      Each <img src={round} alt="legend" style="width:2%" /> is a Piranha specie
    </p>
  </div>

  <svg {width} height={chartHeight}>
    <!-- Axes -->
    <!-- Axis X -->
    <g class="axes">
      {#each ticks as tick}
        <g transform="translate({xScale(tick)}, 0)">
          <text x="0" y={chartHeight - 30} text-anchor="middle">{tick}</text>
          <line x1="0" x2="0" y1="25" y2={chartHeight - 50} stroke="#b9b9b9" />
        </g>
      {/each}
      <text x={chartWidth} y={chartHeight - 5} text-anchor="end"
        >Average size (in cm) →</text
      >
    </g>
    <!-- Axis Y -->
    <g class="axes">
      {#each food as food, i}
        <g transform="translate(40, {yScale(food)})">
          {#if food === "Omnivore, almost herbivore"}
            <rect
              x="-20"
              y="-32"
              width="120"
              height="60"
              fill={colorScale(food)}
            />
            <text
              x="40"
              y="-15"
              text-anchor="middle"
              dominant-baseline="middle"
              class="axis-y"
              fill={i < 2 ? "#fffaf3" : "#172529"}>Omnivore</text
            >
            <text
              x="40"
              y="+15"
              text-anchor="middle"
              dominant-baseline="middle"
              class="axis-y"
              style="font-size:14px"
              fill={i < 2 ? "#fffaf3" : "#172529"}>(almost herbivore)</text
            >
          {:else}
            <rect
              x="-20"
              y="-16"
              width="120"
              height="30"
              fill={colorScale(food)}
            />
            <text
              x="40"
              y="0"
              text-anchor="middle"
              dominant-baseline="middle"
              class="axis-y"
              fill={i < 2 ? "#fffaf3" : "#172529"}>{food}</text
            >{/if}
        </g>
      {/each}
      <text x="30" y="10" text-anchor="start">Diet ↓</text>
    </g>
    <!-- Circles -->
    <g>
      {#each nodes as node}
        <circle
          cx={node.x}
          cy={node.y}
          r={radius}
          fill={colorScale(node.food)}
          stroke="#fffaf3"
        />
      {/each}
    </g>
  </svg>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Fishipedia</p>
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
    color: #172529;
  }

  p {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
    color: #172529;
  }

  .annotation {
    margin-bottom: 0px;
  }

  .axes {
    font-family: "Poppins", sans-serif;
    font-size: 14px;
  }

  .axis-y {
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

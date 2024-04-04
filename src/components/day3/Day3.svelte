<script>
  import { pie, arc } from "d3";
  import { cubicOut } from "svelte/easing";
  import { tweened } from "svelte/motion";
  import logo from "./logo.svg";
  import ItalianPizza from "./ItalianPizza.svelte";
  import Chocolate from "./Chocolate.svelte";
  import Calabrese from "./Calabrese.svelte";
  import Portuguesa from "./Portuguesa.svelte";

  export let width;
  export let height;
  $: chartHeight = height / 1.4;

  let index = 1;
  function animate() {
    if (index === 6) {
      index = 1;
      radius.set(170);
      angle.set(0);
    } else {
      index++;
      radius.set(250);
      if (index === 3) {
        angle.set(1);
      }
    }
  }

  setInterval(function () {
    animate();
  }, 3000);

  const radius = tweened(170, {
    duration: 2000,
    easing: cubicOut,
  });

  const angle = tweened(0, {
    duration: 2000,
    easing: cubicOut,
  });

  //   $: console.log($angle);

  const pieLayout = pie()
    .sort(null)
    .value((d) => d.value);

  $: arcPath = arc().innerRadius(0).outerRadius($radius);

  $: arcs = pieLayout([
    {
      id: "1",
      value: 1,
    },
    {
      id: "2",
      value: $angle,
    },
    {
      id: "3",
      value: $angle,
    },
    {
      id: "4",
      value: $angle,
    },
  ]);

  // $: console.log(index);
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>How to make a brazilian pizza</h2>
    {#if index === 1}<p>
        <span>Step 1:</span> Take an italian pizza
      </p>{:else if index === 2}<p>
        <span>Step 2:</span> Enlarge it
      </p>{:else if index === 3}<p>
        <span>Step 3:</span> Divide it into several parts
      </p>{:else}<p>
        <span>Step 4:</span> Add the recipes of your choice
      </p>{/if}
    <!-- Legend -->
    <svg {width} height="30" class="legend">
      {#if index > 3}<g>
          <g transform="translate({width / 2 - 150} 15)">
            <path
              d="M0 0-70 70A99 99 0 0 1-70-70Z"
              fill="#F45B5D"
              transform="scale(0.2)"
            />
            <text transform="translate(8 0)" dominant-baseline="middle"
              >Savoury recipe</text
            >
          </g>
          <g transform="translate({width / 2 + 20} 15)">
            <path
              d="M0 0-70 70A99 99 0 0 1-70-70Z"
              fill="#4d2904"
              transform="scale(0.2)"
            />
            <text transform="translate(8 0)" dominant-baseline="middle"
              >Sweet recipe</text
            >
          </g>
        </g>
      {/if}
    </svg>
  </div>
  <svg
    viewBox="{-width / 2}, {-height / 2} {width} {height}"
    {width}
    height={chartHeight}
    class="chart"
  >
    <!-- Annotations -->
    {#if index > 3}
      <g class="annotations">
        <text
          transform="translate({-width + 230} {-(height / 2) + 60})"
          dominant-baseline="middle">Chocolate with</text
        >
        <text
          transform="translate({-width + 230} {-(height / 2) + 100})"
          dominant-baseline="middle">strawberries</text
        >
        <text
          transform="translate({-width + 230} {height / 2 - 60})"
          dominant-baseline="middle">Portuguesa</text
        >
        <text
          transform="translate({width - 230} {-(height / 2) + 60})"
          dominant-baseline="middle"
          text-anchor="end">Marguerita</text
        >
        <text
          transform="translate({width - 230} {height / 2 - 60})"
          dominant-baseline="middle"
          text-anchor="end">Calabresa</text
        >
      </g>{/if}

    <g>
      {#each arcs as slice, i}
        <path
          class="center"
          d={arcPath(slice)}
          fill={index > 3 ? (i === 3 ? "#4d2904" : "#F45B5D") : "#F45B5D"}
          stroke={index > 2 ? "#FEC367" : "#FEC367"}
          stroke-width={index > 2 ? "5" : "0"}
        />
        {#if i === 0}
          <ItalianPizza radius={$radius} />
        {/if}
        {#if index > 3}
          {#if i === 3}
            <Chocolate radius={$radius} />
          {/if}
          {#if i === 3}
            <Portuguesa radius={$radius} />
          {/if}
          {#if i === 1}
            <Calabrese radius={$radius} />
          {/if}
        {/if}
      {/each}
    </g>
    <defs>
      <radialGradient id="RadialGradient3">
        <stop offset="92%" stop-color="#FEC367" />
        <stop offset="100%" stop-color="#F99506" />
      </radialGradient>
    </defs>
    <circle
      cx="0"
      cy="0"
      r={$radius}
      stroke="url('#RadialGradient3')"
      stroke-width={$radius * 0.15}
      fill="none"
    />
  </svg>

  <div class="comment">
    <p>Source: My subjective personal experience</p>
  </div>

  <div class="footer">
    <div class="footer-infos">
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
    padding-bottom: 0vh;
  }

  .intro p {
    font-family: "Dancing Script", cursive;
    font-weight: 400;
    font-style: normal;
    font-size: 30px;
    text-align: center;
    width: 100%;
    margin-top: 10px;
    margin-bottom: 10px;
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

  .legend text {
    font-family: "Poppins", sans-serif;
    font-size: 12px;
  }

  .annotations text {
    font-family: "Dancing Script", cursive;
    font-size: 36px;
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

  .comment {
    padding: 0 3vh;
  }

  .comment p {
    font-size: 12px;
    margin: 0;
    font-family: "Poppins", sans-serif;
    padding-top: 8px;
  }

  .challenge {
    background-color: #f45b5d;
    color: #fffaf3;
    padding: 2px 6px;
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
  }

  .logo {
    width: 130px;
  }
</style>

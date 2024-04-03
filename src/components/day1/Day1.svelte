<script>
  import { scaleSqrt } from "d3";
  import data from "./day1_data.json";
  import logo from "./logo.svg";

  export let width;
  export let height;

  $: maxRadius = width / 4.5;
  $: chartHeight = height / 2;
  $: radiusScale = scaleSqrt().domain([0, 260000000]).range([0, maxRadius]);
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>Brazil, the largest lusophone country</h2>
    <p>
      Brazilians represent around 80% of the Portuguese speakers in the world.
      Brazil is one of the countries where Portuguese is the official language,
      along with Angola, Cape Verde, East Timor, Equatorial Guinea,
      Guinea-Bissau, Macau, Mozambique, Portugal and São Tomé and Príncipe.
    </p>
  </div>

  <svg {width} height={chartHeight}>
    <defs>
      <linearGradient id="myGradient" gradientTransform="rotate(90)">
        <stop offset="5%" stop-color="#2c9177" />
        <stop offset="95%" stop-color="#209168" />
      </linearGradient>
    </defs>

    <!-- Circles -->
    <g>
      <!-- World -->
      <circle
        cx={width / 2 - 100}
        cy={chartHeight / 2.2}
        r={radiusScale(data[0].value)}
        fill="#b8d9c6"
      />
      <!-- Brazil -->
      <circle
        cx={width / 2 - 100}
        cy={chartHeight / 2.2 -
          (radiusScale(data[1].value) - radiusScale(data[0].value))}
        r={radiusScale(data[1].value)}
        fill="url(#myGradient)"
      /></g
    >
    <!-- Legend -->
    <g class="legend">
      <!-- World -->
      <rect x={width / 2 + 46} y="15" width="40" height="22" fill="#b8d9c6" />
      <text x={width / 2 + 50} y="15" text-anchor="start">
        <tspan x={width / 2 + 50} dy="1.2em">
          <tspan class="highlight"
            >{Math.round(data[0].value / 1000000) + "M"}</tspan
          >
          portuguese speakers</tspan
        >
        <tspan x={width / 2 + 50} dy="1.2em">in the world (estimation)</tspan>
      </text>
      <line
        x1={width / 2 - 45}
        y1="26"
        x2={width / 2 + 40}
        y2="26"
        stroke="#b8d9c6"
        stroke-width="2"
      />
      <!-- Brasil -->
      <rect
        x={width / 2 + 46}
        y={chartHeight / 2.53 -
          (radiusScale(data[1].value) - radiusScale(data[0].value))}
        width="37"
        height="22"
        fill="#209168"
      />
      <text
        x="0"
        y={chartHeight / 2.2 -
          (radiusScale(data[1].value) - radiusScale(data[0].value))}
        text-anchor="start"
      >
        <tspan x={width / 2 + 50} dy="0em"
          ><tspan class="highlight" fill="#fffaf3"
            >{Math.round(data[1].value / 1000000) + "M"}</tspan
          > Brazilians, speaking</tspan
        >
        <tspan x={width / 2 + 50} dy="1.2em"> portuguese*</tspan>
      </text>
      <line
        x1={width / 2 - 65}
        y1={chartHeight / 2.3 -
          (radiusScale(data[1].value) - radiusScale(data[0].value))}
        x2={width / 2 + 40}
        y2={chartHeight / 2.3 -
          (radiusScale(data[1].value) - radiusScale(data[0].value))}
        stroke="#209168"
        stroke-width="2"
      />
    </g>
  </svg>

  <div class="comment">
    <p>
      * 100% of the population considered, in line with the Obs. da Língua
      Portuguesa
    </p>
    <p>Source: Instituto Camões and World Bank, 2022</p>
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
  }

  h2 {
    font-family: "Londrina Solid", sans-serif;
    font-weight: 400;
    font-size: 2rem;
    margin: 0px 0px;
  }

  p,
  .legend {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
  }

  .highlight {
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
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

<script>
  import logo from "./logo.svg";
  import data from "./data.json";
  import { scaleSqrt, scaleLinear } from "d3";
  import legend1 from "./legend1.png";
  import legend2 from "./legend2.png";

  export let width;
  export let height;
  $: chartHeight = height / 1.8;
  $: chartWidth = width - 50;

  const legend = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May",
    "Jun",
    "Jul",
    "Aug",
    "Sep",
    "Oct",
    "Nov",
    "Dec",
  ];

  // Scales for Radial chart
  const pointScale = scaleSqrt().domain([500, 900000]).range([4, 18]);
  const radiusScale = scaleLinear().domain([2019, 2024]).range([280, 900]);
  const colorScale = scaleLinear([500, 900000], ["#FEC367", "#F99506"]);

  // Scales for bar chart
  const xScale = scaleLinear().domain([2019, 2022]).range([20, 200]);
  const yScale = scaleLinear().domain([0, 530000]).range([20, 70]);
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>International tourism slowly rose again in Brazil after Covid-19</h2>
    <p>
      Monthly view of international tourists visiting Brazil between 2019 and
      2022. During this period, 2020 experienced the the highest number of
      tourists in January (<img
        src={legend1}
        alt="legend-1"
        style="    width: 20px;   margin-bottom: -4px;
        "
      />+870k) and the lowest in May (<img
        src={legend2}
        alt="legend-2"
        style="    width: 12px;   margin-bottom: -1px;
        "
      />517 tourists).
    </p>
  </div>

  <div class="inner-chart">
    <!-- Spiral chart -->
    <svg
      class="chart"
      width={chartWidth}
      height={chartHeight}
      viewBox="0 0 {width} {height}"
    >
      {#if data}
        <g transform="rotate(90">
          {#each data as month, i}
            <circle
              cx={(Math.cos((month.month_id / 13) * 2 * Math.PI + 29.85) *
                radiusScale(month.year)) /
                3 +
                width / 1.9}
              cy={(Math.sin((month.month_id / 13) * 2 * Math.PI + 29.85) *
                radiusScale(month.year)) /
                3 +
                width / 2}
              r={pointScale(month.value)}
              fill={colorScale(month.value)}
            />
          {/each}</g
        >
      {/if}
      {#each legend as month, i}
        <text
          class="highlight"
          x={(Math.cos(((i + 1) / 13) * 2 * Math.PI + 29.85) *
            radiusScale(2023.2)) /
            3 +
            width / 1.9}
          y={(Math.sin(((i + 1) / 13) * 2 * Math.PI + 29.85) *
            radiusScale(2023.2)) /
            3 +
            width / 2}
          text-anchor="middle">{month}</text
        >
      {/each}
      <text
        x={(Math.cos((13 / 13) * 2 * Math.PI + 29.85) * radiusScale(2022)) / 3 +
          width / 1.9}
        y={(Math.sin((13 / 13) * 2 * Math.PI + 29.85) * radiusScale(2022)) / 3 +
          width / 2}
        text-anchor="middle"
        dominant-baseline="hanging">2022</text
      >
      <text
        x={(Math.cos((13 / 13) * 2 * Math.PI + 29.85) * radiusScale(2021)) / 3 +
          width / 1.9}
        y={(Math.sin((13 / 13) * 2 * Math.PI + 29.85) * radiusScale(2021)) / 3 +
          width / 2}
        text-anchor="middle"
        dominant-baseline="hanging">-</text
      >
      <text
        x={(Math.cos((13 / 13) * 2 * Math.PI + 29.85) * radiusScale(2020)) / 3 +
          width / 1.9}
        y={(Math.sin((13 / 13) * 2 * Math.PI + 29.85) * radiusScale(2020)) / 3 +
          width / 2}
        text-anchor="middle"
        dominant-baseline="hanging">2020</text
      >
      <text
        x={(Math.cos((13 / 13) * 2 * Math.PI + 29.85) * radiusScale(2019)) / 3 +
          width / 1.9}
        y={(Math.sin((13 / 13) * 2 * Math.PI + 29.85) * radiusScale(2019)) / 3 +
          width / 2}
        text-anchor="middle"
        dominant-baseline="hanging">-</text
      >
    </svg>
  </div>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Portal Brasileiro de Dados Abertos</p>
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
  }

  .inner-chart {
    display: flex;
    gap: 20px;
  }

  text {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 20px;
  }

  .highlight {
    font-family: "Londrina Solid", sans-serif;
    font-size: 32px;
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
    background-color: #f99506;
    color: #172529;
    padding: 2px 6px;
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
  }

  .logo {
    width: 130px;
  }
</style>

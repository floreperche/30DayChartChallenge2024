<script>
  import logo from "./logo.svg";
  import { scaleLinear, interpolateSpectral } from "d3";
  import data from "./data.json";

  export let width;
  export let height;

  const colorScale = scaleLinear().domain([19.7, 39.7]).range([1, 0]);
  const months = [
    "january",
    "february",
    "march",
    "april",
    "may",
    "june",
    "july",
    "august",
    "september",
    "october",
    "november",
    "december",
  ];

  const legend = Array.from({ length: 150 });
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>Hot N Cold</h2>
    <div class="text-intro">
      <p>
        Among the ten most populated cities in Brazil, one can observe
        significant differences in their climates, based on the maximum
        temperature monthly average.
      </p>
      <div class="annotations">
        <div>Monthly max. temperature</div>
        <div class="legend">
          {#each legend as _, i}
            <div
              class="tone"
              style="height: 8px; width: 1px; background-color: {interpolateSpectral(
                i / legend.length
              )}"
            ></div>
          {/each}
        </div>
        <div class="text-annotations">
          <div style="color:grey">+10°C</div>
          <div style="color:grey">←</div>
          <div>29.7°C*</div>
          <div style="color:grey">→</div>
          <div style="color:grey">-10°C</div>
        </div>
      </div>
    </div>
  </div>

  <div class="inner-chart x-axis">
    <div class="city-line">
      <div class="city"></div>
      {#each months as month}
        <div class="square">{month.slice(0, 3).toUpperCase()}</div>
      {/each}
    </div>
  </div>

  <div class="inner-chart">
    {#each data as data}
      <div class="city-line">
        <div class="city">{data.city} ({data.state})</div>
        {#each months as month}
          <div
            class="square"
            style="background-color: {interpolateSpectral(
              colorScale(data[month])
            )}"
          ></div>
        {/each}
      </div>
    {/each}
  </div>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>*Maximum temperature average in Brazil (yearly)</p>
        <p>Source: Instituto Nacional de Meteorologia, 1991-2020</p>
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

  .text-intro {
    display: flex;
    align-items: center;
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

  .annotations {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 300px;
    gap: 5px;
    font-family: "Poppins", sans-serif;
    font-size: 12px;
    margin-top: 14px;
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

  .inner-chart {
    display: flex;
    flex-direction: column;
    gap: 2px;
    margin-left: 3vh;
  }

  .x-axis {
    font-family: "Londrina Solid", sans-serif;
    margin-bottom: -15px;
    /* background-color: red; */
  }

  .x-axis .square {
    text-align: center;
    line-height: 28px;
  }

  .city-line {
    display: flex;
    gap: 2px;
  }

  .city {
    width: 162px;
    font-family: "Poppins", sans-serif;
    line-height: 28px;
    font-size: 13px;
  }

  .square {
    width: 31px;
    height: 28px;
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

<script>
  import logo from "./logo.svg";
  import { scaleLinear, interpolatePuBuGn } from "d3";
  import data from "./data.json";

  export let width;
  export let height;

  const colorScale = scaleLinear().domain([0, 100]).range([0, 1]);
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
    <h2>Looking for water</h2>
    <div class="text-intro">
      <p>
        Brazil is a humid country, but humidity levels vary greatly among its
        ten most populated cities.
      </p>
      <div class="annotations">
        <div>Relative humidity</div>
        <div class="legend">
          {#each legend as _, i}
            <div
              class="tone"
              style="height: 8px; width: 1px; background-color: {interpolatePuBuGn(
                i / legend.length
              )}"
            ></div>
          {/each}
        </div>
        <div class="text-annotations">
          <div>0%</div>
          <div>50%</div>
          <div>100%</div>
        </div>
        <div style="display:flex; align-items:center; gap:10px;">
          <div style="width:20px; height:10px; background-color: #b9b9b9"></div>
          <p style="font-size:12px;margin-top:0px">Missing information</p>
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
            style="background-color: {data[month] > 0
              ? interpolatePuBuGn(colorScale(data[month]))
              : '#b9b9b9'}"
          ></div>
        {/each}
      </div>
    {/each}
  </div>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Instituto Nacional de Meteorologia,</p>
        <p>1991-2020 (and 1981-2020 for Rio de Janeiro)</p>
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

  .text-intro > p {
    padding-right: 70px;
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
    margin-bottom: -10px;
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

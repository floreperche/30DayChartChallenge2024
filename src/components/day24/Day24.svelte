<script>
  import logo from "./logo.svg";
  import viz from "./viz.png";

  export let width;
  export let height;
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>Where is produced the cocoa of your favorite chocolate?</h2>
    <p>
      The ten largest cocoa producing countries in 2022, and their volume of
      production in 1972 and 2022 (tonnes)
    </p>
  </div>

  <div class="chart"><img src={viz} alt="visualization" /></div>
  <div class="comment">
    <p>
      Source: Food and Agriculture Organization of the United Nations (2023) via
      Our World in Data
    </p>
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
    color: #172529;
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
  .comment {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 14px;
  }

  .comment {
    padding: 0 3vh;
  }

  .intro p {
    margin-bottom: 0px;
  }

  .chart {
    padding: 0vh 3vh;
    display: flex;
    justify-content: center;
  }

  .chart img {
    width: 100%;
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

<script>
  import logo from "./logo.svg";
  import viz from "./viz.png";

  export let width;
  export let height;

  const rect = Array.from({ length: 20 });
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>Brazil, a key player of renewable energy consumption</h2>
    <p>
      In 2022, almost half (48%) of the primary energy consumed in Brazil came
      from renewable sources. It ranks it as the third-best country in the world
      in terms of renewable energy usage, mainly with hydropower energy.
    </p>
  </div>

  <div class="chart"><img src={viz} alt="visualization" /></div>
  <div class="comment">
    <p>
      Source: Energy Institute - Statistical Review of World Energy (2023) via
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
    margin-bottom: -20px;
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

  .comment {
    padding: 0 3vh;
    margin-bottom: -10px;
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

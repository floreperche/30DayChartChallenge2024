<script>
  import logo from "./logo.svg";
  import graph from "./graph.png";

  export let width;
  export let height;
  $: chartHeight = height / 2;
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>In thirty years, meat consumption nearly doubled in Brazil</h2>
    <p>
      Between 1992 and 2022, meat consumption per inhabitant increased by 80%.
      During that period, poultry meat became the most consumed meat.
    </p>
  </div>

  <div class="graph"><img src={graph} alt="Graph of meat consumption" /></div>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: OECD-FAO Agricultural Outlook 2023-2032</p>
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
    padding-bottom: 0px;
  }

  .intro p {
    margin-bottom: 0px;
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

  .graph {
    padding: 0vh 3vh;
  }

  .graph img {
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

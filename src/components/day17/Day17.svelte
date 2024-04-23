<script>
  import logo from "./logo.svg";
  import map from "./map.png";

  export let width;
  export let height;
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>River basins in Brazil</h2>
  </div>

  <div class="map"><img src={map} alt="Map of Brazil" /></div>

  <div class="comment">
    <p>Tutorial from Milos Makes Maps</p>
    <p>Source: ©World Wildlife Fund, Inc. (2006-2013) HydroSHEDS database</p>
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
    background-color: #03131b;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    color: #cef6cd;
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

  .map {
    padding: 0vh 3vh;
    display: flex;
    justify-content: center;
  }

  .map img {
    width: 75%;
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
    padding-top: 0.5vh;
  }

  .comment p {
    font-size: 12px;
    margin: 0;
  }

  .challenge {
    background-color: #5ab959;
    color: #03131b;
    padding: 2px 6px;
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
  }

  .logo {
    width: 130px;
  }
</style>

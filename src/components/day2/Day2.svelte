<script>
  import logo from "./logo.svg";
  import map from "./map.png";

  export let width;
  export let height;
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>The unique design of Brasília</h2>
    <p>
      Brasília, the capital of Brazil, was built from scratch between 1956 and
      1960, at the request of the President Juscelino Kubitschek. Both The urban
      planner Lucio Costa and the architect Oscar Niemeyer designed the initial
      and distinctive outline and architecture of the city.
    </p>
  </div>

  <div class="map"><img src={map} alt="Map of Brasilia" /></div>

  <div class="comment">
    <p>Source: Open Street Map, Unesco</p>
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
    background-color: #271b45;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    color: #fffaf3;
  }

  .intro {
    padding: 3vh;
    padding-bottom: 0vh;
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
  }

  .map img {
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
  }

  .comment p {
    font-size: 12px;
    margin: 0;
  }

  .challenge {
    background-color: #fffaf3;
    color: #271b45;
    padding: 2px 6px;
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
  }

  .logo {
    width: 130px;
  }
</style>

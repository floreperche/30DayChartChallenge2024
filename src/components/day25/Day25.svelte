<script>
  import logo from "./logo.svg";
  import map from "./map.png";
  import cardinal from "./orientation.png";

  export let width;
  export let height;
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>A change of perspective</h2>
    <div class="cardinal"><img src={cardinal} alt="Cardinal points" /></div>
  </div>

  <div class="map">
    <img src={map} alt="World map with the South at the top of the view" />
  </div>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: World Bank Official Boundaries</p>
      </div>
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
    display: flex;
    justify-content: space-between;
    /* background-color: red; */
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

  .cardinal {
    /* background-color: blue; */
    width: 90px;
    padding-top: 5px;
  }

  .cardinal img {
    width: 100%;
  }

  .map {
    padding: 0vh 0.5vh;
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

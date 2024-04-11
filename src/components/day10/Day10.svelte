<script>
  import logo from "./logo.svg";
  import chart from "./graph.png";
  import legend from "./legend.png";

  export let width;
  export let height;
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>Where do the most renowned Brazilian wines come from?</h2>
    <div class="text-elements">
      <p>
        Ten Brazilian wine regions have been recognized by geographical
        indications. More than half of them are from Rio Grande do Sul, and two
        benefit from the more restrictive 'DO' designation.
      </p>
      <div class="legend">
        <img src={legend} alt="legend" />
        <div>
          <p>Wine region located in Rio Grande do Sul</p>
          <p>Wine region located in another state</p>
        </div>
      </div>
    </div>
  </div>

  <div class="chart">
    <img src={chart} alt="Chart" />
    <div class="categories">
      <p>Indicação de procedência (IP)¹</p>
      <p class="do">Denominação de Origem (DO)²</p>
    </div>
  </div>

  <div class="annotations">
    <p>
      ¹ Geographical regognition for a tipical product of the region.
      <br />
      ² Restrictive recognition for a region producing a product with certain qualities
      or caracteristics.
    </p>
  </div>

  <div>
    <div class="footer">
      <div class="footer-infos">
        <div class="comment">
          <p>Source: Empresa Brasileira de Pesquisa Agropecuária</p>
        </div>
        <p class="challenge">#30DayChartChallenge 2024</p>
      </div>
      <img src={logo} alt="wild variables logo" class="logo" />
    </div>
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
    padding-bottom: 0;
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

  .text-elements {
    display: flex;
    gap: 25px;
  }

  .text-elements > p {
    width: 70%;
    margin: 0;
    font-size: 13px;
  }

  .legend {
    display: flex;
    width: 35%;
    align-items: center;
    gap: 5px;
  }

  .legend img {
    width: 70%;
    height: 80%;
  }

  .legend p {
    font-size: 10px;
    margin-top: 0;
  }

  .legend div {
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 4px;
  }

  .chart {
    padding: 0vh 3vh;
  }

  .chart img {
    width: 100%;
  }

  .categories {
    display: flex;
    justify-content: center;
    gap: 120px;
  }

  .categories p {
    width: 120px;
    text-align: center;
    font-size: 18px;

    font-family: "Londrina Solid", sans-serif;
  }

  .annotations {
    padding-left: 3vh;
    padding-right: 3vh;
  }

  .annotations p {
    font-size: 10px;
    margin-bottom: 0;
    margin-top: 0;
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

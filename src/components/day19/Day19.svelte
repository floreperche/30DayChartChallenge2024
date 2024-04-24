<script>
  import logo from "./logo.svg";
  import viz from "./viz.png";

  export let width;
  export let height;
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>Older than a dinosaur</h2>
    <p>
      Paleontologists from the Laboratório de Paleobiologia at Universidade
      Federal do Pampa found the skull of an amphibian on a farm in Rio Grande
      do Sul, Brazil, in 2022.
    </p>
    <p>
      Revealed at the beggining of 2024, the specie named <i>Kwatisuchus</i> lived
      before the dinosaurs, approximately 250 million years ago. Surprisingly, analysis
      revealed connections with other species discovered in Russia.
    </p>
  </div>

  <div class="chart"><img src={viz} alt="visualization" /></div>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Universidade Federal do Pampa & futura-sciences</p>
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
    color: #1d3c3f;
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
    background-color: #1d3c3f;
    color: #fffaf3;
    padding: 2px 6px;
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
  }

  .logo {
    width: 130px;
  }
</style>

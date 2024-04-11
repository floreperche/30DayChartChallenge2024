<script>
  import logo from "./logo.svg";
  import amphibiants from "./amphibiants.png";
  import birds from "./birds.png";
  import fishes from "./fishes.png";
  import mammals from "./mammals.png";
  import reptiles from "./reptiles.png";
  import plants from "./plants.png";
  import legend from "./legend.png";

  export let width;
  export let height;
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <div class="text-elements">
      <h2>The highest biodiversity country</h2>
      <p>
        <span>Brazil</span> ranks in almost every Top 5 of the most diverse countries
        for each biodiversity category. Cumulatively, it is the country with the
        highest biodiversity, ahead of Indonesia and China.
      </p>
    </div>

    <div class="legend">
      <img src={legend} alt="legend" />
      <p>Category</p>
    </div>
  </div>

  <div class="chart">
    <div>
      <img src={amphibiants} alt="amphibiants" />
      <p>Amphibiants</p>
    </div>
    <div>
      <img src={birds} alt="birds" />
      <p>Birds</p>
    </div>
    <div>
      <img src={fishes} alt="fishes" />
      <p>Fishes</p>
    </div>
    <div>
      <img src={mammals} alt="mammals" />
      <p>Mammals</p>
    </div>
    <div>
      <img src={reptiles} alt="reptiles" />
      <p>Reptiles</p>
    </div>
    <div>
      <img src={plants} alt="plants" />
      <p>Plants</p>
    </div>
  </div>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Mongabay, World Rainforests 2024</p>
      </div>
      <p class="challenge">#30DayChartChallenge 2024</p>
    </div>
    <img src={logo} alt="wild variables logo" class="logo" />
  </div>
</div>

<style>
  .chart-container {
    background-color: #012824;
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

  .intro {
    display: flex;
    justify-content: space-between;
  }

  .text-elements {
    margin-bottom: 0px;
    width: 70%;
  }

  .intro span {
    color: #fc4873;
    font-weight: 600;
  }

  .legend {
    width: 27%;
    display: flex;
    flex-direction: column;
    height: fit-content;
    padding: 2vh 0;
  }

  .legend img {
    width: 100%;
    height: 100%;
  }

  .legend p {
    margin: 0 auto;
    text-align: center;
    font-family: "Londrina Solid", sans-serif;
    font-size: 18px;
    padding: 1vh;
  }

  .chart {
    padding: 0 3vh;
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: space-between;
  }

  .chart div {
    width: 27%;
    display: flex;
    flex-direction: column;
  }

  .chart img,
  .intro img {
    width: 100%;
    height: 80%;
  }

  .chart p {
    margin: 0 auto;
    padding: 1vh;
    font-family: "Londrina Solid", sans-serif;
    font-size: 18px;
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
    color: #012824;
    padding: 2px 6px;
    font-family: "Londrina Solid", sans-serif;
    font-size: 16px;
  }

  .logo {
    width: 130px;
  }
</style>

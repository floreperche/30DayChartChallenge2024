<script>
  import logo from "./logo.svg";
  import data from "./data.json";
  import { scaleOrdinal } from "d3";

  export let width;
  export let height;

  const waffle = Array.from({ length: 100 });

  const colorRange = ["#F2DBB7", "#1D7454", "#6CBD88"];

  const colorScale = scaleOrdinal()
    .domain([data.map((e) => e.id)])
    .range(colorRange);
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <div class="intro">
    <h2>
      Whatsapp, the main communication channel between companies and clients in
      Brazil
    </h2>
    <p>
      Whatsapp is the most used app in Brazil. Initially adressed to private
      conversations, it has become a key tool for professionnal communications
      too.
    </p>
  </div>

  <div class="chart">
    <div class="waffle" style="width:{width / 2}px">
      {#each waffle as _, index}
        <svg width="30" height="30">
          <path
            d="M161 322C249.918 322 322 249.918 322 161C322 72.0822 249.918 0 161 0C72.0822 0 0 72.0822 0 161C0 183.381 4.56684 204.696 12.8195 224.063L0.387937 322.088L90.3853 305.728C111.706 316.15 135.67 322 161 322Z"
            fill={index < data[0].value
              ? "#1D7454"
              : index < data[0].value + data[1].value
                ? "#6CBD88"
                : "#F2DBB7"}
            transform="scale(0.07)"
          /></svg
        >
      {/each}
    </div>

    <div class="legend">
      <div>
        <p>
          <span
            style="background-color : {colorScale(data[0].id)}; color: #fffaf3"
            >{data[0].value}%</span
          >
          {data[0].category}
        </p>
      </div>

      <div>
        <p>
          <span
            style="
            background-color : {colorScale(data[1].id)}; 
            color: #172529">{data[1].value}%</span
          >
          {data[1].category}
        </p>
        <p>
          <span
            style="background-color : {colorScale(data[2].id)}; color : #172529"
            >{data[2].value}%</span
          >
          {data[2].category}
        </p>
      </div>
    </div>
  </div>

  <div class="footer">
    <div class="footer-infos">
      <div class="comment">
        <p>Source: Opinion Box survey, 2023</p>
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
    display: flex;
    gap: 20px;
    padding-left: 3vh;
    padding-right: 3vh;
  }

  .waffle {
    display: flex;
    flex-wrap: wrap;
  }

  .legend {
    width: 40%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 10px;
  }

  .legend div {
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding-bottom: 8px;
  }

  .legend p {
    margin: 0;
  }

  .legend span {
    padding: 0px 4px;
    font-family: "Londrina Solid", sans-serif;
    font-size: 20px;
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

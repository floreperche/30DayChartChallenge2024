<script>
  export let data;
  export let colorScale;
  export let map;
  const waffle = Array.from({ length: 100 });
  //   console.log(data);
  const value = data.percentage;
</script>

<div class="graph">
  <p class="name">{data.region}</p>

  <div class="map">
    <img src={map} alt="Map of {data.region}" />
    <p class="data" style="background-color : {colorScale(data.region)} ">
      {data.percentage}%
    </p>
    <p>({Math.round(data.population / 1000000) + "M"} inhabitants)</p>
  </div>

  <div class="waffle">
    {#each waffle as _, index}
      <div
        class="square"
        style="background-color : {index < value
          ? colorScale(data.region)
          : '#F2DBB7'}"
      ></div>
    {/each}
  </div>
</div>

<style>
  .graph {
    display: flex;
    flex-direction: column;
    gap: 26px;
    width: 100px;
  }

  .name {
    font-weight: 600;
  }

  .map {
    position: relative;
  }

  img {
    width: 100%;
  }

  .waffle {
    display: flex;
    flex-wrap: wrap-reverse;

    gap: 3px;
  }

  .square {
    width: 7px;
    height: 7px;
  }

  p {
    width: fit-content;
    font-family: "Poppins", sans-serif;
    font-size: 13px;
    margin: 0px;
  }

  .map p {
    font-size: 10px;
  }

  .map .data {
    font-family: "Londrina Solid", sans-serif;
    letter-spacing: 1px;
    padding: 2px 4px;
    font-size: 16px;
    color: #fffaf3;
    position: absolute;
    bottom: 24px;
    left: 0px;
  }
</style>

<script>
  export let yScale;
  export let xScale;

  const ticks = Array.from({ length: 20 });

  //   $: console.log(ticks);
</script>

<g class="axis-y">
  {#each ticks as tick, i}
    <g class="tick">
      <text
        x="6"
        y={yScale(i + 1)}
        dominant-baseline="middle"
        text-anchor="middle"
        style="font-size : {3 / (i + 1) + 10}px">{i + 1}</text
      >
      <line
        x1={xScale(2013.5)}
        x2={xScale(2023.2)}
        y1={yScale(i + 1)}
        y2={yScale(i + 1)}
        stroke="#b9b9b9"
        stroke-width="0.4"
        stroke-opacity={i % 2 === 0 ? "100%" : "50%"}
      />
      {console.log(i % 2)}
    </g>
  {/each}
  <text
    class="axis-title"
    x="3"
    y="0"
    text-anchor="start"
    dominant-baseline="hanging"
    dy="1"
    style="    font-size: 12px;
    ">↑ Rank in the Brasileirão Série A Championship</text
  >
  <g>
    <line
      x1={xScale(2013.5)}
      x2={xScale(2023.2)}
      y1={yScale(6.22)}
      y2={yScale(6.22)}
      stroke="#0884BD"
      stroke-width="2"
      stroke-dasharray="8"
    />
    <line
      x1={xScale(2013.5)}
      x2={xScale(2023.2)}
      y1={yScale(6.66)}
      y2={yScale(6.66)}
      stroke="#E4050F"
      stroke-width="2"
      stroke-dasharray="8"
    /></g
  >
</g>

<style>
  text {
    font-family: "Poppins", sans-serif;
    font-size: 12px;
  }
</style>

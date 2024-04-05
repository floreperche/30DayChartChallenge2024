<script>
  export let width;
  export let xScale;
  export let yScale;
  export let data;
</script>

<defs>
  <linearGradient id="gradient" gradientTransform="rotate(90)">
    <stop offset="0%" stop-color="#fffaf300" />
    <stop offset="10%" stop-color="#fffaf3" />
  </linearGradient>
</defs>
<g class="axis-x">
  <rect
    x={xScale(2014)}
    y={yScale(20)}
    {width}
    height="100"
    fill="url('#gradient')"
  />
  {#each data as tick}
    <g class="tick" transform="translate({xScale(tick.year)},0)">
      <text x="0" y={yScale(22)} text-anchor="middle">{tick.year}</text>
      <line x1="0" x2="0" y1={yScale(20.5)} y2={yScale(21)} stroke="black" />
    </g>
  {/each}
  <text
    class="axis-title"
    x={xScale(2023.3)}
    y={yScale(22.2)}
    text-anchor="end"
    dominant-baseline="hanging"
    dy="8">Championship year →</text
  >
</g>

<style>
  text {
    font-family: "Poppins", sans-serif;
    font-size: 12px;
  }
</style>

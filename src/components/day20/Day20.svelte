<script>
  import viz from "./viz.png";
  export let width;
  export let height;
</script>

<div style="width: {width}px; height: {height}px" class="chart-container">
  <img src={viz} alt="visualisation" />
</div>

<style>
  .chart-container {
    background-color: #fffaf3;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
</style>
